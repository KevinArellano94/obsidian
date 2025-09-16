#10x #software #engineering #architecture #scalable #robust #enterprise

## Application Architecture

Our goal should be to have division in between specific functionality, but maintaining domain-driven development (DDD) that allows related things to live together.

Naming convention should be redundant ( @[[Redundancy as a Feature]] ) yet descriptive, to allow searchability to be as simple as possible.

### Example

Let's go ahead and create our project file structure for an a inventory management system utilizing apollo graphql named Kraken.

```markdown
kraken/
├── src/
│   ├── domain/
│   │   ├── product/
│   │   │   ├── product.repository.ts
│   │   │   ├── product.resolver.ts
│   │   │   ├── product.schema.ts
│   │   │   └── product.service.ts
│   │   └── user/
│   └── utils/
│       ├── auth.ts
│       └── logger.ts
├── deps.ts
└── main.ts
.gitignore
Dockerfile
README.md
```

### Software Roadmap

At the first sight of this, it might seem overzealous and verbose. Though there is a reason behind the madness, this aids on the search functionality and allows extremely easily the location of where one is working on in any given time.

The blueprint, though, on the logic behind the naming convention is as follows:

```typescript
repository // The closest code that interacts with the data source (e.g. databases)
service // The business logic layer, value validation and transformation
schema // Required type-definition for graphql to understand the data structure
resolver // The invocable query/mutation that the user will call
```

I can already hear "but Kevin, I can write this in a single line of code". Yes, you are correct! You can even ditch the whole concept all together and it would still `work`. We're here not to find the shortest none-scalable way in getting things done, but the contrary.

The goal here is to `divide` where we'll be working on in any point-in-time. Needing to add a new feature that allows batch insertion? Adding it to the repository doesn't break anything! Needing to update the business logic? You don't have to worry about updating the database schema. How do I create unit testing for this complex resolver? You don't have to anymore, each `domain` is it's own thing, you can test each individual component fluidly.

![[Pasted image 20250830155412.png]]

### Implementation

Reverse engineering, literally! Start with the data source and work towards the user facing implementation.

product.repository.ts

```typescript
import { MongoClient, Collection, ObjectId } from "https://deno.land/x/mongo@v0.31.2/mod.ts";

export interface Product {
    _id: ObjectId;
    name: string;
    description: string;
    price: number;
    inventory_count: number;
    created_at: Date;
    updated_at: Date;
}

export class ProductRepository {
    private dbPromise: Promise<Collection<Product>>;
  
    constructor() {
        this.dbPromise = getDbClient();
    }
  
    public async findAll(): Promise<Product[]> {
        const db = await this.dbPromise;
        const allProducts = await db.find().toArray();
        return allProducts;
    }
  
    public async createOne(productData: Product) {
        const collection = await this.dbPromise;
        const now = new Date();
  
        const documentToInsert: Omit<Product, '_id'> = {
            ...productData,
            created_at: now,
            updated_at: now,
        };
  
        const insertId = await collection.insertOne(documentToInsert);
  
        const newProduct: Product = {
            '_id': insertId,
            ...documentToInsert,
        }
  
        return newProduct;
    }
}
```

product.service.ts

```typescript
import { Product, ProductRepository } from './product.repository.ts';
  
export class ProductService {
    private productRepository: ProductRepository;
  
    constructor() {
        this.productRepository = new ProductRepository();
    }
  
    public async getAllProducts(): Promise<Product[]> {
        return await this.productRepository.findAll();
    }
  
    public async createOneProduct(product: Product): Promise<Product> {
        return await this.productRepository.createOne(product);
    }
}
```

product.schema.ts

```typescript
import { gql } from '../../deps.ts';
  
export const ProductTypeDefs = gql`#graphql
    type Product {
        name: String
        description: String
        price: String
        inventory_count: Int
        created_at: String
        updated_at: String
    }
  
    input InputProduct {
        name: String
        description: String
        price: String
        inventory_count: Int
        created_at: String
        updated_at: String
    }
  
    type Query {
        products: [Product]
    }
  
    type Mutation {
        addProduct(input: InputProduct): Product
    }
`;
```

product.resolver.ts

```typescript
import { Product } from './product.repository.ts';
import { ProductService } from './product.service.ts';
  
const productService: ProductService = new ProductService();
  
export const ProductQueryResolvers = {
    products: async(_: any, __: any, context: any, ____: any): Promise<Product[]> => {
        try {
            return await productService.getAllProducts();
        } catch (error: unknown | any) {
            throw new Error(error);
        }
    },
}
  
export const ProductMutationResolvers = {
    addProduct: async(_: any, __: any, context: any, ____: any): Promise<Product> => {
        try {
            const input = __.input;
            return await productService.createOneProduct(input);
        } catch (error: unknown | any) {
            throw new Error(error);
        }
    },
}
```