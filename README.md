這個項目是一個簡易的線上圖書館系統，旨在展示領域驅動設計(DDD)在NestJS應用中的實踐，特別是使用ORM作為基礎架構層(repository)的一部分，並且將ORM entity直接作為領域層(domain)的實體(entity)
。

功能特點
書籍管理：包括書籍的增加、查詢、借閱和歸還。
會員管理：實現會員的註冊與資料更新。
借閱記錄：記錄並展示借閱歷史。

# Simplified DDD Practice Guide

This GitHub repository offers a tutorial on how to implement Domain-Driven Design (DDD) in a simplified manner for small-scale projects, specifically utilizing Mikro-ORM as a direct repository mechanism. It aims to provide a clear and easy-to-understand approach to DDD practices.

## Project Background

In Domain-Driven Design (DDD), there's typically a strong emphasis on the separation between the Domain Layer and the Infrastructure Layer. However, in small-scale or educational projects, adhering strictly to this separation can introduce unnecessary complexity. This example shows a simplified approach, using an ORM framework as a bridge between the Domain Layer and the Infrastructure Layer, focusing on Mikro-ORM for its direct integration capabilities.

## Key Concepts

- **Domain Model**: Reflects the core concepts of business logic and rules, directly mapped to the database structure and managed by Mikro-ORM.
- **ORM as Repository**: Simplifies data operations and business logic implementation by using the ORM's capabilities as the repository layer.

## Project Structure

```
├── src/
│   ├── domain/
│   │   ├── entities/         - Defines domain entities
│   │   │   └── Book.ts       - 书籍实体
│   │   └── interfaces/       - 领域服务接口（如果有）
│   │
│   ├── application/
│   │   ├── dtos/             - 数据传输对象定义
│   │   │   └── CreateBookDto.ts
│   │   ├── services/         - 应用服务
│   │   │   └── BookService.ts
│   │   └── interfaces/       - 应用服务接口（如REST API控制器）
│   │
│   └── infrastructure/
│       ├── orm/              - ORM配置和实体映射
│       │   └── mikro-orm.config.ts
│       └── repositories/     - 实体仓库实现（可选，由Mikro-ORM管理）
```

## Installation

Install the project dependencies:

```bash
$ npm install
```

## Running the App

- **Development mode**:

  ```bash
  $ npm run start
  ```

- **Watch mode**:

  ```bash
  $ npm run start:dev
  ```

- **Production mode**:

  ```bash
  $ npm run start:prod
  ```

## Testing

- **Unit tests**:

  ```bash
  $ npm run test
  ```

- **End-to-end (e2e) tests**:

  ```bash
  $ npm run test:e2e
  ```

- **Test coverage**:

  ```bash
  $ npm run test:cov
  ```

## Getting Started

1. **Define Domain Entities** in the `/src/domain/entities` directory. For example, a `Book` entity:

   ```typescript
   // /src/domain/entities/Book.ts
   import { Entity, PrimaryKey, Property } from '@mikro-orm/core';

   @Entity()
   export class Book {
     @PrimaryKey()
     id!: number;

     @Property()
     title: string;

     @Property()
     author: string;

     constructor(title: string, author: string) {
       this.title = title;
       this.author = author;
     }
   }
   ```

2. **Implement Application Services** in the `/src/application` directory to coordinate domain logic:

   ```typescript
   // /src/application/bookService.ts
   import { Injectable } from '@nestjs/common';
   import { EntityManager } from '@mikro-orm/core';
   import { Book } from '../domain/entities/Book';

   @Injectable()
   export class BookService {
     constructor(private readonly em: EntityManager) {}

     async addNewBook(title: string, author: string): Promise<Book> {
       const book = a new Book(title, author);
       await this.em.persistAndFlush(book);
       return book;
     }
   }
   ```

## Conclusion

This example is designed to help beginners understand the core concepts of Domain-Driven Design and quickly implement business logic by directly using an ORM as a repository. It's hoped that this simplified practice will deepen your understanding and application of DDD.