# Introduction

Zod is a TypeScript-first schema declaration and validation library.

Zod is designed to be as developer-friendly as possible. The goal is to eliminate duplicative type declarations.

# Installation

### requirement

-   typescript 4.5 or higher
-   tsconfig.json

    ```typeScript
    {
        /...
        compilerOptions: {
            /...
            strict:true,
        }
    }

    ```

### From npm

```npm
npm install zod
```

# Basic Usage

creating a simple string schema

```ts
import { z } from 'zod';
// creating a basic string schema
const mySchema = z.string();
//parsing
mySchema.parse('hello'); // 'hello'
mySchema.parse(123); // throws a zod error
// "safe" parsing (doesn't throw error if validation fails)
mySchema.safeParse('tuna'); // => { success: true; data: "tuna" }
mySchema.safeParse(12); // => { success: false; error: ZodError }
```

creating a object schema

```ts
import { z } from 'zod';
// creating a  object schema
const myObj = z.object({
    name: z.string(),
    age: z.number(),
});

//parsing
myObj.parse({ name: 'tuna', age: 12 }); // {name:'tuna',age:12}

//extract the inferred type
type myObj = z.infer<typeof myObj>;
// => {name:string,age:number}
```

# Primitives

```ts
import { z } from 'zod';

// primitive values
z.string();
z.number();
z.bigint();
z.boolean();
z.date();
z.symbol();

// empty types
z.undefined();
z.null();
z.void(); // accepts undefined

// catch-all types
// allows any value
z.any();
z.unknown();

// never type
// allows no values
z.never();
```

# Coercion for primitives

Zod provides a more convenient way to coerce primitive values.

```ts
const schema = z.coerce.string();
schema.parse('tuna'); // => "tuna"
schema.parse(12); // => "12"
```

During the parsing step, the input is passed through the String() function, which is a JavaScript built-in for coercing data into strings.

```ts
schema.parse(12); // => "12"
schema.parse(true); // => "true"
schema.parse(undefined); // => "undefined"
schema.parse(null); // => "null"
```

The returned schema is a normal ZodString instance so you can use all string methods.

```ts
z.coerce.string().email().min(5);
```

** How Coercion Works**

All primitive types support coercion. Zod coerces all inputs using the built-in constructors: `String(input)`, `Number(input)`, `new Date(input)`, etc.

```ts
z.coerce.string(); // String(input)
z.coerce.number(); // Number(input)
z.coerce.boolean(); // Boolean(input)
z.coerce.bigint(); // BigInt(input)
z.coerce.date(); // new Date(input)
```

_Note_
:Boolean coercion with z.coerce.boolean() may not work how you expect. Any truthy value is coerced to true, and any falsy value is coerced to false.

```ts
const schema = z.coerce.boolean();

schema.parse(1); // => true
schema.parse('tuna'); // => true
schema.parse('true'); // => true
schema.parse('false'); // => true
schema.parse([]); // => true

schema.parse(0); // => false
schema.parse(''); // => false
schema.parse(undefined); // => false
schema.parse(null); // => false
```

# Literals
