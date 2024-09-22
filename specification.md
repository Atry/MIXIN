# MIXIN Language Specification

## 1. Introduction

MIXIN (Multi-language Interoperable eXtensive Interface Notion) is a programming language designed to facilitate the flexible composition and configuration of logic and data structures through the use of _mixins_. Unlike traditional programming languages that use classes or functions as the primary building blocks, MIXIN employs a unified concept where everything is represented as a mixin. This approach allows for greater modularity, reusability, and flexibility.

MIXIN is a lazily-evaluated, immutable language, meaning that values are only computed when necessary, and once created, they cannot be changed. This design makes MIXIN particularly well-suited for applications that require functional purity, such as configuration management, domain-specific language (DSL) creation, and code generation.

MIXIN is not limited to a specific platform or target language. It can generate code for multiple languages by representing abstract syntax trees (ASTs) that correspond to various programming languages. This makes MIXIN an ideal choice for scenarios involving cross-language interoperability, complex configuration files, and even software synthesis.

### 1.1 Comparison with Other Languages

#### 1.1.1 Object-Oriented Languages

In traditional object-oriented languages like Java or C++, classes and objects are used to encapsulate state and behavior. However, this approach has several limitations that MIXIN addresses through its unique design:

- **Complex Inheritance Hierarchies**: Object-oriented languages often require complex class hierarchies to represent different behaviors, leading to rigidity and difficulty in maintenance. Multiple inheritance, in particular, can introduce the "diamond problem," where the same method or property is inherited from multiple sources, causing ambiguity and conflicts.

  - **MIXIN Solution**: MIXIN uses a flexible composition model where mixins can be combined and inherited without conflict. Properties are automatically merged, and there is no need for complex inheritance trees. This eliminates the diamond problem and allows for clean, modular inheritance structures.

- **Static and Inflexible Object Models**: Once a class is defined in an object-oriented language, its structure and behavior are fixed. Modifying or extending the behavior often requires creating subclasses or using design patterns like decorators, which can add complexity and reduce clarity.

  - **MIXIN Solution**: Mixins in MIXIN can be dynamically composed and configured, allowing for flexible adjustments without altering existing definitions. This dynamic composition model enables developers to easily modify and extend behavior by combining mixins, without the need for static class hierarchies or complex design patterns.

- **Method Overriding and the Risk of Ad Hoc Behavior**: Traditional object-oriented languages rely on method overriding to modify inherited behavior. This can lead to unpredictable behavior, especially in deep inheritance hierarchies, where methods in subclasses may inadvertently override those in parent classes, introducing subtle bugs.

  - **MIXIN Solution**: MIXIN does not support method overriding. Instead, it merges properties from multiple parent mixins, ensuring that all inherited properties coexist without conflict. This approach avoids the risks associated with method overriding, such as accidental method shadowing or breaking polymorphic behavior, providing a more predictable and safer inheritance model.

- **Overreliance on Design Patterns**: To address limitations in object-oriented design, developers often resort to complex design patterns like Singleton, Factory, and Strategy. While these patterns solve specific problems, they can introduce additional complexity and boilerplate code.

  - **MIXIN Solution**: MIXIN can be seen as a metaprogramming language designed to generate code for other languages. Instead of using design patterns to address language limitations, developers can use MIXIN to generate consistent and reusable code across multiple languages. By representing abstract syntax trees (ASTs) and configurations as mixins, MIXIN allows for the creation of domain-specific languages (DSLs) and the automated generation of language constructs, reducing the need for complex design patterns and enabling more expressive and maintainable code.

Overall, MIXIN provides a more modular and flexible alternative to traditional object-oriented languages by using mixin composition instead of class inheritance. Its support for property merging and dynamic composition allows developers to build complex systems more easily and safely. As a metaprogramming language, MIXIN excels in generating code for multiple languages, making it a powerful tool for scenarios requiring cross-language interoperability and code generation.

#### 1.1.2 Functional Languages

Functional programming languages like Haskell and Scala emphasize immutability and functional purity, offering benefits such as easier reasoning about code and avoidance of side effects. However, they also come with certain limitations that MIXIN addresses through its design:

- **Complexity of Function Composition Syntax**: Functional languages often use advanced and abstract syntax for function composition, such as higher-order functions, monads, and combinators. While powerful, these constructs can be difficult to read and understand, especially for those new to functional programming.

  - **MIXIN Solution**: MIXIN employs a more intuitive and declarative approach by representing logic and data structures through mixin composition and configuration. Using familiar data serialization formats like YAML or JSON, MIXIN allows developers to define complex behaviors in a hierarchical and readable manner. This reduces the syntactic complexity associated with function composition in traditional functional languages.

- **Complexity of Context Management**: In functional programming, managing context, such as state or environment, often requires explicit passing of context through function parameters or using monads, which can make code verbose and harder to maintain.

  - **MIXIN Solution**: MIXIN simplifies context management by allowing mixins to automatically inherit and reference properties from their lexical scope. This means that shared context or state can be accessed without the need for explicit parameter passing or complex monadic structures. The unified scoping and referencing rules in MIXIN reduce boilerplate code and make the logic more straightforward.

- **The Expression Problem**: The Expression Problem refers to the difficulty of extending both the set of data types and the set of operations over them in a type-safe and modular way. In functional languages, adding new data types is straightforward, but adding new operations can be challenging without modifying existing code.

  - **MIXIN Solution**: MIXIN addresses the Expression Problem by allowing both mixins (representing data types) and properties or methods (representing operations) to be extended and composed modularly. Since mixins can inherit and combine properties from multiple sources without conflicts, developers can add new data types and operations independently. This flexibility enables MIXIN to support extensibility in both dimensions, overcoming the limitations faced in traditional functional programming languages.

Overall, MIXIN provides a more accessible and flexible alternative to functional programming languages by reducing syntactic complexity, simplifying context management, and addressing the Expression Problem. Its mixin-based composition model allows for the modular and conflict-free extension of both data structures and operations, facilitating the development of complex systems in a more intuitive and maintainable way.

#### 1.1.3 Declarative Configuration Languages

Declarative configuration languages like JSON, YAML, and Nix are widely used to represent static data and configurations. They offer simplicity and readability but often lack the ability to express dynamic logic and complex relationships. MIXIN extends these ideas, providing a more powerful and flexible alternative.

- **Static Configuration Limitations**: Traditional configuration languages like JSON and YAML are limited to representing static data structures. They cannot express dynamic relationships or logic, such as conditional values, calculations, or dependencies between configurations.

  - **MIXIN Solution**: MIXIN allows for dynamic logic and configuration through mixin composition and inheritance. Properties can be inherited, combined, or overridden based on context, enabling dynamic configurations that adapt to changing conditions. This makes MIXIN suitable for scenarios where complex dependencies and conditional configurations are required.

- **Lack of Modularity and Reusability**: In static configuration formats, it is difficult to create modular and reusable components. While YAML supports features like anchors and aliases, these are limited and can lead to complex and error-prone configurations.

  - **MIXIN Solution**: MIXIN enables modular and reusable configuration components through its mixin system. Each mixin can encapsulate a piece of configuration or logic, which can then be combined and reused in different contexts. This modular approach not only improves maintainability but also allows for the creation of complex configurations by composing simpler, reusable mixins.

- **Difficulty in Representing Relationships**: Declarative configuration languages often lack the ability to represent complex relationships between different parts of a configuration. Dependencies, references, and relationships must be managed manually, which can lead to errors and inconsistencies.

  - **MIXIN Solution**: MIXIN uses references to represent relationships between mixins, enabling clear and maintainable configurations. By using a unified reference and inheritance model, MIXIN allows for the automatic resolution of dependencies and relationships, reducing the risk of errors and inconsistencies.

- **Limited Expressiveness for Code Generation**: While declarative languages like Nix provide some level of code generation through lazy evaluation and functional constructs, they are primarily designed for configuration management and package management. Extending them for general-purpose code generation or complex logical expressions can be cumbersome.

  - **MIXIN Solution**: MIXIN, as a metaprogramming language, is designed to generate code and configurations for multiple target languages. By representing abstract syntax trees (ASTs) and logical structures as mixins, MIXIN can be used to generate code in different languages consistently. This capability makes MIXIN ideal for building DSLs, automating code generation, and ensuring consistency across different language environments.

Overall, MIXIN extends the capabilities of traditional declarative configuration languages by supporting dynamic logic, modularity, and complex relationships. Its mixin-based approach enables more expressive and maintainable configurations, and its metaprogramming capabilities make it a powerful tool for code generation and cross-language interoperability.

### 1.2 Key Use Cases

#### 1.2.1 Multi-language Code Generation

MIXIN can generate code in multiple target languages, making it a versatile tool for building DSLs or serving as the core module of a compiler. By representing the ASTs of various languages as mixins, MIXIN can translate a single logical structure into multiple programming languages, ensuring consistency and reducing duplication across projects.

#### 1.2.2 Cross-language Interoperability

MIXIN provides a unified way to define data structures and logic that can be shared across different programming environments. For instance, a complex business logic model defined in MIXIN can be translated into both a backend service in Scala and a frontend component in JavaScript, ensuring consistent behavior and data flow.

#### 1.2.3 Complex System Configuration

As a configuration language, MIXIN excels in defining complex systems with interdependent components. Through the use of mixin composition and inheritance, configuration files can be modular, reusable, and adaptable, enabling powerful and flexible system configurations that go beyond the capabilities of traditional static formats like JSON or YAML.

### 1.3 A Simple Example

The following example demonstrates how to use MIXIN to define a basic arithmetic operation represented as an AST:

````yaml
# math_operations.mixin.yaml

Number:
  - {} # A mixin that represents a number type.

add:
  - [Number] # Inherits from the 'Number' mixin.
  - addend1: [Number] # Property 'addend1', which is a 'Number'.
  - addend2: [Number] # Property 'addend2', which is also a 'Number'.

multiply:
  - [Number] # Inherits from the 'Number' mixin.
  - multiplicand: [Number] # Property 'multiplicand', which is a 'Number'.
  - multiplier: [Number] # Property 'multiplier', which is also a 'Number'.```
````

```yaml
# test.mixin.yaml

example_calculation:
  - [add]
  - addend1:
      - [multiply]
      - multiplicand: 2
      - multiplier: 3
  - addend2: 4
```

**Explanation**:

1. The `Number` mixin represents a basic number type with no initial value, aligning with MIXIN's immutable and lazy-evaluated nature.
2. The `add` mixin inherits from `Number` and defines two properties, `addend1` and `addend2`, both of which are also `Number`.
3. The `multiply` mixin defines a multiplication operation with two properties: `multiplicand` and `multiplier`.
4. In `test.mixin.yaml`, the `example_calculation` mixin uses the `add` operation to add two numbers:
   - `addend1` is a multiplication of `2` and `3`, represented using the `multiply` mixin.
   - `addend2` is the constant `4`.

This example illustrates how MIXIN can be used to represent complex logic in a modular and declarative manner. The `example_calculation` mixin serves as the root of an AST, with each operation (e.g., `add` and `multiply`) acting as nodes, and their properties (`addend1`, `addend2`, `multiplicand`, `multiplier`) as sub-nodes. This structure can be evaluated directly within MIXIN or used to generate equivalent code in another language.

## 2. Mixin Definitions and Data Types

### 2.1 Basic Structure and Data Types

MIXIN supports a range of data types, all of which map directly to JSON data types. These types form the foundational elements of the language and define how data is represented and manipulated within MIXIN.

#### 2.1.1 Primitive Data Types

The primitive data types in MIXIN correspond directly to JSON’s scalar types:

- **Strings**: Represented as sequences of characters, corresponding to JSON strings.

  - Example: `"hello, world"`

- **Numbers**: Can be either integers or floating-point numbers, just like JSON numbers.

  - Example: `42`, `3.14`

- **Booleans**: Represent truth values, with `true` and `false` as the only valid values.

  - Example: `true`, `false`

- **Null**: Represents the absence of a value, similar to JSON `null`.
  - Example: `null`

#### 2.1.2 Mixins as Data Types

In MIXIN, the primary data type is the mixin itself, which corresponds to JSON objects. Each mixin represents a collection of properties and can inherit from other mixins, enabling complex compositions and configurations.

- **Mixin**: Corresponds to a JSON object, with each key representing a property name and each value representing a mixin, primitive type, or a reference to another mixin.

  Example:

  ```yaml
  Number:
    - {} # A mixin with no properties, representing a number type.

  add:
    - [Number] # Inherits from the 'Number' mixin.
    - addend1: [Number] # Property 'addend1', which is a 'Number'.
    - addend2: [Number] # Property 'addend2', which is also a 'Number'.
  ```

  In this example:

  - The `Number` mixin serves as a base mixin with no initial properties.
  - The `add` mixin inherits from `Number` and introduces two new properties, `addend1` and `addend2`, both of which are of type `Number`.

#### 2.1.3 Relationship to JSON

MIXIN's data types map directly to JSON types:

- **JSON Object → Mixin**: A mixin is defined by a JSON object where keys are property names, and values can be mixins or primitive data types.
- **JSON Scalar Types → Primitive Data Types**: JSON strings, numbers, booleans, and null values map directly to MIXIN's corresponding primitive data types.

#### 2.1.4 No First-class List Support

Unlike JSON, MIXIN does not support lists as a first-class type within the language itself. This means that you cannot directly define or manipulate lists in the core MIXIN language as you would in JSON. Instead, lists are defined and manipulated through the MIXIN standard library. This design choice maintains the simplicity and consistency of the language by focusing on mixin composition and inheritance. For scenarios requiring list-like structures or operations, MIXIN encourages using custom mixins to represent collections or sequences of data.

### 2.2 Properties

Properties are the fundamental components of a mixin, defining its internal state or behavior. The value of a property can be one of the following types:

1. **Basic Data Types**: Strings, numbers, booleans, or null.
2. **References (Inheritance)**: Properties can reference other mixins by specifying their path, allowing for inheritance and reuse of existing mixins.

#### Property Definition Syntax

The definition of a property resembles key-value pairs in JSON or YAML. Unlike most programming languages, property names in MIXIN do not need to be unique. If the same property name is defined multiple times, all definitions will always be automatically merged through multiple inheritance. This allows for the creation of complex and modular structures without conflict.

Example:

```yaml
Person:
  - name: [String] # Defines a 'name' property of type String
  - age: [Number] # Defines an 'age' property of type Number
  - is_married: [Boolean] # Defines an 'is_married' property of type Boolean
```

In this example, if `name` is defined again in a different mixin and both mixins are inherited, the resulting mixin will contain all definitions of `name`.

#### Nested Properties

Property values can be nested mixins, creating more complex structures. For example, we can define an `Address` property within the `Person` mixin:

```yaml
Address:
  - street: [String] # Defines a 'street' property
  - city: [String] # Defines a 'city' property
  - zip_code: [String] # Defines a 'zip_code' property

person_with_address:
  - [Person] # Inherits the 'Person' mixin
  - address: [Address] # Adds an 'address' property using the 'Address' mixin
```

In this example, the `person_with_address` mixin inherits from `Person` and includes a nested `address` property that references the `Address` mixin.

### 2.3 References and Inheritance

In MIXIN, references and inheritance are equivalent concepts. By referencing another mixin, the current mixin inherits all properties and scalar values from the referenced mixin. A reference is represented as an array of strings that indicate the path to the target mixin.

#### Grouping Property Definitions in Lists

When defining a mixin, you can optionally put properties in lists, i.e. the `-` symbol in YAML, to indicate the hierarchical structure of properties. When a mixin inherits from other mixins, properties must be prefixed with `-` to avoid confusion between inheritance chains and property declarations. This prefix is optional when there is no inheritance.

**Why Use the `-` Prefix for Properties**

In YAML, a node must be either an array or an object; it cannot contain both array elements and object members simultaneously. Therefore, when a mixin inherits other mixins, the `-` prefix is required to clearly indicate that each property is an item in an array. This prefix is optional when there is no inheritance but is mandatory when inheritance is involved.

**Invalid YAML**:

```yaml
my_car:
  - [Vehicle]          # Inherits the 'Vehicle' mixin
  color: [String]    # Adds a new property 'color'
  doors: [Number]    # Adds a new property 'doors'
```

In the example above, the `my_car` node simultaneously contains an array element (`[Vehicle]`) and object members (`color` and `doors`), which violates the structural rules of YAML.

**Valid YAML**:

```yaml
my_car:
  - [Vehicle] # Inherits the 'Vehicle' mixin
  - color: [String] # Adds a new property 'color'
  - doors: [Number] # Adds a new property 'doors'
```

In this valid example, each element within the `my_car` node begins with the `-` prefix, indicating that these properties are part of an array. This allows the YAML parser to correctly interpret the structure of `my_car`.

#### Multiple Inheritance and Scalar Values

MIXIN supports conflict-free multiple inheritance and allows scalar values to be inherited from multiple sources. This means a mixin can combine properties and scalar values from multiple parent mixins without any conflict. All inherited properties and values are integrated seamlessly, resulting in a unified set of properties for the child mixin.

**Example of Multiple Inheritance with Scalar Values**

MIXIN allows scalar values to coexist and be inherited along with other properties, as shown below:

```yaml
Number:
  - {} # Defines an empty number type mixin

my_number:
  - 42 # Defines the scalar value 42
  - [Number] # Inherits the 'Number' mixin
```

In this example, `my_number` has both a scalar value `42` and inherits the `Number` type mixin, demonstrating that scalar values and type mixins can coexist and be inherited together.

**Conflict-Free Inheritance**

In MIXIN, properties with the same name defined in multiple parent mixins are always automatically merged:

```yaml
# basic_features.mixin.yaml
Vehicle:
  - wheels: [Number]
  - engine: {}

Motor:
  - engine:
      gasoline: true # Defines a default scalar value for 'engine'

# advanced_features.mixin.yaml
hybrid_car:
  - ["basic_features", Vehicle]
  - ["basic_features", Motor]
  - wheels: 4 # Defines the scalar value for 'wheels'
  - engine:
      hybrid: true # Defines the scalar value for 'engine'
  - battery_capacity: 100 # Adds a new 'battery_capacity' property
```

In this example, `hybrid_car` inherits the `engine` property from both `Vehicle` and `Motor`. Instead of a conflict, the properties are merged, along with its extra property hybrid, which the child mixin explicitly defines. The `battery_capacity` property is added uniquely to `hybrid_car`.

## 3. Syntax and Grammar

### 3.1 Lexical Structure

MIXIN is a language that leverages the lexical structures of JSON, YAML, and TOML, focusing on their ability to represent structured data in a clear and readable manner. This section outlines the core syntax and grammar of MIXIN, emphasizing its usage of these formats and how they correspond to MIXIN's data and logic constructs.

MIXIN does not have its own unique lexical structure; instead, it directly adopts the lexical structures of JSON, YAML, and TOML. This means that any syntax that can be converted into JSON is valid in MIXIN. Specifically:

- **JSON**: Fully supported, including all standard JSON types and structures.

- **YAML**: Supported as long as it can be losslessly converted into JSON. This means that only a subset of YAML is used, excluding features such as:

  - **Anchors and Aliases**: YAML constructs like `&` (anchor) and `*` (alias) are not supported as they cannot be directly represented in JSON.
  - **Tags**: YAML's type tags (e.g., `!!str`, `!!int`) are not supported, as MIXIN uses its own data type system.
  - **Complex Data Types**: Data types like sets, timestamps, and ordered mappings are not supported.

- **TOML**: Supported in its JSON-compatible subset, which includes basic data types like strings, finite numbers, booleans, and dates, but excludes date / time datatypes.

By utilizing these existing formats, MIXIN ensures a seamless integration with widely-used data serialization standards, making it easy to define complex data structures and configurations.

#### 3.1.1 Examples of Supported and Unsupported Syntax

**Supported JSON Syntax**:

```json
{
  "name": "example",
  "value": 42,
  "is_active": true,
  "data": null
}
```

**Supported YAML Syntax**:

```yaml
name: example
value: 42
is_active: true
data: null
```

**Unsupported YAML Syntax** (anchors and aliases):

```yaml
base: &base_value
  name: example

derived:
  <<: *base_value
  value: 42
```

**Supported TOML Syntax**:

```toml
name = "example"
value = 42
is_active = true
```

**Unsupported TOML Syntax** (time):

```toml
data = 23:22:21.0123
```

## 4. File Structure and Formats

### 4.1 Supported File Formats

MIXIN supports the following file formats for representing source code:

- **YAML**: File extension `.mixin.yaml`.
- **JSON**: File extension `.mixin.json`.
- **TOML**: File extension `.mixin.toml`.

MIXIN uses these formats to define mixins in a structured and human-readable manner. The formats share the following characteristics:

1. **JSON Compatibility**: All supported formats must be serializable to JSON. This means that only the subset of YAML and TOML that can be converted to JSON without loss of information is supported.

2. **File Extensions**: The file extension must indicate the format and its use as a MIXIN file, such as `.mixin.yaml`, `.mixin.json`, or `.mixin.toml`.

3. **Lossless Conversion**: The language only uses features that can be converted between the supported formats without loss of information.

### 4.2 File and Mixin Naming Conventions

#### 4.2.1 File Naming Conventions

- **Format**: Use lowercase letters with underscores to separate words. File names must include the `.mixin.` segment to indicate they are MIXIN files.

- **Type Definition**: Use singular nouns if defining a primary concept (e.g., `vehicle.mixin.yaml`). Use plural nouns if the file contains multiple instances or variations (e.g., `vehicles.mixin.yaml`).

**Examples**:

- `vehicle.mixin.yaml`
- `vehicles.mixin.yaml`
- `test_cases.mixin.json`

#### 4.2.2 Mixin Naming Conventions

Mixin names within files must follow these conventions based on their intended use:

1. **Type-like Mixins**:

   - Use UpperCamelCase naming (e.g., `PersonDetails`, `Vehicle`). These mixins represent types and can be inherited by other mixins.
   - Should not include scalar values; instead, focus on defining structured data or behaviors.

2. **Value-like Mixins**:

   - Use lowercase with underscores (e.g., `height_value`, `name`). These mixins typically represent individual values or instances and may include scalar values.

3. **Instance Mixins**:

   - Use lowercase with underscores (e.g., `electric_vehicle`, `combined_person`) to represent specific instances or configurations and may inherit from multiple type-like mixins.

### 4.3 Cross-File References

MIXIN allows referencing mixins defined in different files. The rules for cross-file references are as follows:

1. **Reference Format**:

   - A reference is represented as an array of strings, where each string corresponds to a segment in the path to the target mixin.
   - The format for cross-file references is `[path, to, mixin_name]`, where `path` is the relative path from the current file to the target mixin, excluding the top-level directory name.

2. **Directory Scope**:

   - Each directory has its own lexical scope. Files within the same directory can reference each other using just the file name and mixin name (e.g., `[file_name, mixin_name]`).
   - Directories do not share scopes, meaning that each directory’s scope is independent. A mixin defined in one directory cannot directly reference a sibling directory’s mixin without specifying the correct path.

3. **Lexical Scope Resolution**:

   - MIXIN automatically searches for references starting in the current directory. If not found, it searches in the parent directory, and then the parent's parent directory, continuing upwards until the root is reached.
   - The first segment of the reference looks for the mixin name in the current lexical scope, which includes:

     - **Current File**: Mixins defined in the same file.
     - **Parent Mixins**: Mixins in the parent scope of the current mixin.
     - **Directory Scope**: Mixins defined directly in the current directory.

   - Subsequent segments can reference properties in the inherited mixin hierarchy if the first segment resolves to a mixin in the scope.

4. **Isolated File Scopes**:

   - Mixins defined in separate files within the same directory do not share lexical scopes with each other. They can only access mixins from the directory scope and their own file.

5. **No `..` Syntax for Parent Directory**:

   - MIXIN does not support the `..` syntax to navigate to parent directories. Instead, the language automatically searches upward through the directory structure, starting from the current directory.

#### 4.3.1 Example of Cross-File References

**Directory Structure**:

```
project/
│
├── module/
│   ├── vehicle.mixin.yaml
│   ├── electric.mixin.yaml
│   └── car.mixin.yaml
│
├── config/
│   └── settings.mixin.yaml
└── test/
    └── test_car.mixin.yaml
```

**vehicle.mixin.yaml**:

```yaml
Vehicle:
  engine: {}
  wheels: [Number]
```

**electric.mixin.yaml**:

```yaml
Electric:
  - engine：
       electric: true
  - battery_capacity: [Number]
```

**car.mixin.yaml**:

```yaml
Car:
  - [Vehicle]
  - [Electric]
  - model: [String]
```

**test_car.mixin.yaml**:

```yaml
test_car:
  - [module, Car] # Cross-directory reference to Car in module/car.mixin.yaml
  - model: "Test Model"
  - test_battery:
      - [module, Electric, battery_capacity] # Reference to battery_capacity in Electric
```

In this example:

- The `test_car` mixin in `test_car.mixin.yaml` references `Car` and `Electric` in the `module` directory using the format `[module, Car]` and `[module, Electric, battery_capacity]`.
- The first segment of the reference (`module`) indicates the directory in which the target mixins are located.
- The reference format and scope rules ensure that mixins are correctly resolved based on the file and directory structure.

### 4.4 Best Practices for File Organization

1. **Modular File Organization**:

   - Organize mixin definitions into separate files based on functionality and domain, such as `vehicle.mixin.yaml` and `person.mixin.yaml`.
   - Use directories to group related files, such as `src`, `tests`, and `examples`.

2. **Clear Naming Conventions**:

   - Ensure that file and mixin names clearly reflect their contents and purpose. Avoid using generic names that do not convey the mixin’s role.

3. **Use of Directory Scope**:

   - Take advantage of directory scope for organizing large projects. Define common mixins at the directory level and use file-level mixins for specific configurations or instances.

4. **Avoid Excessive Cross-References**:

   - Minimize the use of cross-file references to maintain modularity and reduce complexity. Use directory-level mixins to share common definitions.

5. **Testing and Validation**:

   - Regularly validate mixin files against the MIXIN JSON Schema to ensure correct syntax and structure.
   - Use the MIXIN Nix runtime to test and evaluate mixin configurations before deployment.

## 5. Scope and Reference Resolution

### 5.1 Scope Definition

In the MIXIN language, scope determines the visibility and reference relationships of mixins and properties within the current context. The scope structure includes sibling mixins, parent mixins, directory scope, and cross-file references.

**Scope in MIXIN consists of the following levels**:

- **Sibling Mixins**: The names of other mixins in the same file are visible in the current scope and can be referenced using the format `[mixin_name]`. References to sibling mixins take precedence over parent mixin references.

- **Parent Mixins**: The names of all parent mixins in the current hierarchy are visible in the current scope. A mixin can access its parent mixins but not itself. If a property within a mixin references its containing mixin, it can do so because the containing mixin is in the enclosing scope.

- **Directory Scope**: A directory has a lexical scope that includes all mixins defined directly within that directory. Files within the directory can access mixins in the directory’s scope using the format `[directory_name, mixin_name]`.

- **Cross-File References**: When referencing mixins across different directories, the path must include the relative path from the current file to the target mixin.

MIXIN does not distinguish between types and values. Any mixin can represent either a data value or a type. However, in practice, type-like mixins are usually named using the UpperCamelCase convention and represent structures or behaviors to be inherited. Value-like mixins are named using lowercase letters with underscores and typically represent individual values or instances.

### 5.2 Reference Resolution and Inheritance

References in MIXIN are resolved **dynamically at the time of mixin evaluation or inheritance**. The first segment of the reference determines how the target is identified based on the current context.

#### 5.2.1 First Segment Resolution

- **First Segment is an Outer Mixin**: If the first segment references an outer mixin (e.g., `[Outer, sibling]`), it behaves like `Outer.this.sibling` in Java, meaning it explicitly references the `sibling` property of the `Outer` mixin. This is useful when you want to access a mixin defined in an enclosing scope.

- **First Segment is a Sibling Mixin**: If the first segment references a sibling mixin (e.g., `[sibling, sibling_property]`), it behaves like `this.sibling.sibling_property` in Java, meaning it references the `sibling` mixin in the current context and then accesses `sibling_property`. This allows you to reference mixins defined alongside the current mixin.

- **First Segment Resolution in Lexical Scope**:

  - The first segment of the reference searches for the mixin name in the current lexical scope, which includes:

    - **Current File**: Mixins defined within the same file.

    - **Parent Mixins**: Mixins in the parent scope of the current mixin.

    - **Directory Scope**: Mixins defined directly within the current directory.

  - **No Inheritance Lookup in First Segment**: The first segment does not search for properties within inherited mixins.

#### 5.2.2 Subsequent Segment Resolution

After resolving the first segment, subsequent segments can reference properties within the inherited mixin hierarchy.

- **Inherited Properties**: Subsequent segments can access properties inherited from parent mixins.

- **Dynamic Resolution**: References are resolved dynamically, meaning that if inherited mixins are extended or overridden in the current context, the reference reflects these changes.

#### 5.2.3 Reference Resolution Example

Consider the following example:

```yaml
OuterMixin:
  inner_mixin:
    property: "value"

CurrentMixin:
  - [OuterMixin]
  - reference_to_inner:
      - [OuterMixin, inner_mixin]  # References 'inner_mixin' in 'OuterMixin'
  - reference_to_sibling:
      - [sibling_mixin, property]  # References 'property' in 'sibling_mixin'
  sibling_mixin:
    property: "sibling value"
```

In this example:

- **`reference_to_inner`** uses `[OuterMixin, inner_mixin]`:

  - **First Segment**: `OuterMixin`, which is an outer mixin in the current scope.

  - **Resolution**: It behaves like `OuterMixin.this.inner_mixin`, accessing the `inner_mixin` defined in `OuterMixin`.

- **`reference_to_sibling`** uses `[sibling_mixin, property]`:

  - **First Segment**: `sibling_mixin`, which is a sibling mixin defined in the same file.

  - **Resolution**: It behaves like `this.sibling_mixin.property`, accessing the `property` in `sibling_mixin`.

#### 5.2.4 Cross-Directory References

When referencing mixins across different directories, the path must include relative path segments:

```yaml
- [path, to, mixin_name, property]
```

- **First Segment**: `path` is interpreted relative to the directory structure of the current file.

- **Resolution**: MIXIN will automatically search for the referenced mixin by traversing the directory hierarchy.

### 5.3 Multiple Inheritance and Scalar Value Handling

MIXIN supports **conflict-free multiple inheritance**, allowing mixins to inherit properties and scalar values from multiple parent mixins without conflicts. This feature enables the flexible composition of complex structures by combining the functionalities of various mixins.

#### 5.3.1 Inheritance and Property Merging

When a mixin inherits from multiple parent mixins, the properties from all parents are **merged** into the child mixin. If multiple parent mixins define the same property, the definitions are automatically combined, avoiding naming conflicts and preserving all inherited behaviors.

**Example:**

```yaml
# basic_features.mixin.yaml
Vehicle:
  - wheels: [Number]
  - engine: {}

Motor:
  - engine: {}

# advanced_features.mixin.yaml
hybrid_car:
  - ["basic_features", Vehicle]
  - ["basic_features", Motor]
  - wheels: 4 # Defines the scalar value for 'wheels'
  - engine: # Merging with 'Vehicle.engine'
      hybrid: true
  - battery_capacity: 100 # Adds a new 'battery_capacity' property
```

In this example:

- **Inheritance**:
  - `hybrid_car` inherits from both `Vehicle` and `Motor`.
- **Property Merging**:
  - The `engine` property is defined in both parent mixins.
  - MIXIN automatically merges the `engine` property without conflict.
- **Resulting Properties**:
  - `hybrid_car` has access to all properties from both parents: `wheels`, `engine`, and `battery_capacity`.

#### 5.3.2 Scalar Value Merging

Scalar values (e.g., strings, numbers, booleans) can coexist with properties within a mixin and can be inherited from multiple parent mixins. MIXIN does not define specific rules for merging scalar values from different parents; instead, scalar values from all parents are included in the child mixin without causing errors. The **specific merging behavior** of scalar values is defined by the libraries used in conjunction with MIXIN, allowing for different strategies depending on the application's needs.

**Example:**

```yaml
# number.mixin.yaml
Number:
  - {} # Represents a number type mixin

# value.mixin.yaml
value_42:
  - 42 # Defines scalar value 42

# my_number.mixin.yaml
my_number:
  - [Number]
  - [value_42]
```

In this example:

- **Inheritance**:
  - `my_number` inherits from both `Number` and `value_42`.
- **Scalar Value Coexistence**:
  - Combines the scalar value `42` and any properties from `Number`.
- **No Conflict**:
  - Scalar values and properties coexist without conflict in `my_number`.

#### 5.3.3 Merging Scalar Values with Properties

A mixin can have both scalar values and properties, and these can be inherited from multiple parents. MIXIN allows this combination without conflicts, enabling more expressive and flexible mixin definitions.

**Example:**

```yaml
# person.mixin.yaml
PersonDetails:
  name: [String]
  age: [Number]

# height.mixin.yaml
height_value: 180 # Scalar value representing height

# combined_person.mixin.yaml
combined_person:
  - [PersonDetails]
  - name: "John Doe"
  - age: 30
  - [height_value]
```

In this example:

- **Inheritance**:
  - `combined_person` inherits from both `PersonDetails` and `height_value`.
- **Combined Properties and Scalar Values**:
  - Includes properties `name` and `age`, and scalar value `180`.
- **No Conflict**:
  - Both properties and scalar values are accessible without conflict.

#### 5.3.4 Conflict-Free Inheritance

MIXIN's approach to inheritance ensures that properties and scalar values from multiple parents are merged seamlessly. This conflict-free inheritance model eliminates issues commonly associated with multiple inheritance in other languages, such as the diamond problem.

- **Automatic Merging**: Properties with the same name are automatically merged.
- **No Overwriting**: Scalar values and properties from different parents do not overwrite each other unless explicitly redefined in the child mixin.
- **Flexibility**: Developers can compose mixins freely without worrying about inheritance conflicts.

**Example of Conflict-Free Inheritance:**

```yaml
# basic_features.mixin.yaml
Vehicle:
  - wheels: [Number]
  - engine:
      gasoline: true # Scalar value for 'engine'

Motor:
  - engine: {} # Defines 'engine' property

# advanced_features.mixin.yaml
hybrid_car:
  - ["basic_features", Vehicle]
  - ["basic_features", Motor]
  - wheels: 4 # Scalar value for 'wheels'
  - engine: # Merging with 'Vehicle.engine'
      hybrid: true
  - battery_capacity: 100 # New property
```

In this example:

- **Inheritance**:
  - `hybrid_car` inherits from both `Vehicle` and `Motor`.
- **Property Merging**:
  - Merges `engine` properties from parents.
- **Resulting Properties**:
  - Combines properties `wheels`, `engine`, and `battery_capacity` in `hybrid_car`.

### 6. Binding Rules and Examples

References in MIXIN can be resolved using either **early binding** or **late binding** mechanisms. Understanding these binding rules is crucial for determining how mixins and properties are inherited and resolved during evaluation. The following example illustrates the differences between early and late binding within a single mixin structure.

### 6.1 Example

Consider the following MIXIN definition:

```yaml
test_binding:
  my_mixin1:
    - inner:
        field1: "value1"
    - early_binding:
        - [test_binding, my_mixin1, inner] # Early binding to 'inner' in 'my_mixin1'
    - late_binding:
        - [my_mixin1, inner] # Late binding to 'inner' in 'my_mixin1'
    - late_binding_too:
        - [inner] # Late binding within the same mixin

  my_mixin2:
    - [my_mixin1]
    - inner:
        field2: "value2"
```

### 6.2 Explanation of Binding Mechanisms

#### 6.2.1 Early Binding

- **Definition**: Early binding resolves references at the time of mixin definition. The reference remains fixed and does not change even if the mixin is inherited or extended in different contexts.

- **Behavior in Example**:

  - `test_binding.my_mixin1.early_binding` references `[test_binding, my_mixin1, inner]`. This means it always points to the original `inner` mixin defined within `my_mixin1`, regardless of how `my_mixin1` is inherited or extended.

- **Result**:

  - `test_binding.my_mixin2.early_binding` contains only `field1` because it references the original `my_mixin1.inner`, which has only `field1`. It does not adapt to the additional `field2` added in `my_mixin2.inner`.

#### 6.2.2 Late Binding

- **Definition**: Late binding resolves references dynamically at the time of mixin evaluation or inheritance. The reference adapts to the current context, including any changes made through inheritance or property merging.

- **Behavior in Example**:

  - `test_binding.my_mixin1.late_binding` references `[my_mixin1, inner]`. When inherited by `my_mixin2`, this reference dynamically resolves to `my_mixin2.inner`, which includes both `field1` and `field2`.

  - Similarly, `test_binding.my_mixin1.late_binding_too` references `[inner]` within the same mixin. When inherited by `my_mixin2`, it also resolves to `my_mixin2.inner`, which now contains both `field1` and `field2`.

- **Result**:

  - Both `test_binding.my_mixin2.late_binding` and `test_binding.my_mixin2.late_binding_too` contain both `field1` and `field2`, as the late-bound references adapt to the current context of `my_mixin2.inner`.
    Here is the continuation of the translation for sections 6.2.3, 6.3, and 6.4:

### 6.2.3 Key Observations

1. **Early Binding**:

   - **Fixed Reference**: Always points to the originally defined mixin or property.
   - **Example Behavior**: `test_binding.my_mixin2.early_binding` only includes `field1` because it references the original `my_mixin1.inner` and does not adapt to changes in `my_mixin2`.

2. **Late Binding**:

   - **Dynamic Reference**: Adapts to the current mixin context, including any inherited or merged properties.
   - **Example Behavior**: Both `test_binding.my_mixin2.late_binding` and `test_binding.my_mixin2.late_binding_too` include both `field1` and `field2` because they reference `my_mixin2.inner`, which dynamically includes all fields.

3. **The First Segment Determines the Resolution Method**:

   - If the first segment references an outer mixin (e.g., `[test_binding, my_mixin1, inner]`), it uses early binding, behaving like an explicit reference to a specific mixin.
   - If the first segment references a sibling mixin or the current context (e.g., `[my_mixin1, inner]` or `[inner]`), it uses late binding and is dynamically resolved based on the current mixin’s inheritance and context.

### 6.3 Practical Guidelines

To effectively use early and late binding in MIXIN:

- **Use Early Binding When**:

  - You need a reference to always point to a specific mixin or property, regardless of how the mixin is inherited or extended.
  - You want to ensure that a property remains constant and unaffected by changes in the inheritance hierarchy.

- **Use Late Binding When**:
  - You want references to adapt dynamically based on the context in which the mixin is used.
  - You are building mixins intended for reuse and extension, where properties may be added or merged.

### 6.4 Summary

In MIXIN, choosing between early and late binding allows you to control how references are resolved during inheritance and evaluation:

- **Early Binding**: Ensures a fixed reference that remains constant across all contexts.
- **Late Binding**: Provides flexibility by adapting to the current context, making it suitable for dynamic and extensible mixin definitions.

By understanding these binding rules and how the first segment of a reference determines the resolution mechanism, you can design mixins that behave predictably and flexibly, depending on your use case.

## 7. Appendices

This section provides additional resources and references to aid in the understanding of the MIXIN language. It includes a JSON Schema reference, which defines the structure of MIXIN files, and a glossary of terms used throughout the language specification.

### 7.1 JSON Schema Reference

The following JSON Schema defines the structure of MIXIN files. It specifies the types and constraints for mixin definitions, including references, properties, and inheritance rules. This schema is useful for validating MIXIN files to ensure they conform to the expected format.

```json
{
  "$schema": "https://json-schema.org/draft-07/schema",
  "title": "MIXIN Language Schema",
  "$ref": "#/definitions/mixin",
  "definitions": {
    "reference": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "minItems": 1,
      "description": "A MIXIN reference, represented as an array of strings."
    },
    "properties": {
      "type": "object",
      "description": "A collection of property definitions.",
      "additionalProperties": {
        "$ref": "#/definitions/mixin"
      }
    },
    "inheritancesAndOwnProperties": {
      "type": "array",
      "description": "An array representing a combination of super mixins, properties, or nested structures.",
      "items": {
        "oneOf": [
          {
            "$ref": "#/definitions/reference"
          },
          {
            "$ref": "#/definitions/properties"
          },
          {
            "$ref": "#/definitions/inheritancesAndOwnProperties"
          }
        ]
      }
    },
    "mixin": {
      "description": "A mixin",
      "oneOf": [
        {
          "$ref": "#/definitions/reference"
        },
        {
          "$ref": "#/definitions/properties"
        },
        {
          "$ref": "#/definitions/inheritancesAndOwnProperties"
        },
        {
          "type": "string"
        },
        {
          "type": "number"
        },
        {
          "type": "boolean"
        },
        {
          "type": "null"
        }
      ]
    }
  }
}
```

#### Explanation of the Schema

- **Reference**:

  - Represents a reference to another mixin or module. Defined as an array of strings. This format is used to point to other mixins within the same file or across files.
  - Example: `[module_name, mixin_name]` or `[file_name, mixin_name]`.

- **Properties**:

  - Represents a collection of property definitions within a mixin. Each property can be another mixin or a scalar value (string, number, boolean, or null).
  - Example:
    ```yaml
    person:
      name: "John Doe"
      age: 30
      is_employed: true
    ```

- **Inheritances and Own Properties**:

  - Represents a combination of inheritance and property definitions within a mixin. This allows a mixin to inherit from other mixins while also defining its own properties.
  - Example:
    ```yaml
    Car:
      - [Vehicle]
      - model: "Sedan"
      - color: "Blue"
    ```

- **Mixin**:
  - Represents a mixin definition. A mixin can be a reference to another mixin, a set of properties, or a combination of inheritance and properties.

This schema provides a structured way to define and validate mixins in the MIXIN language, ensuring consistency and correct syntax across different files and formats.

### 7.2 Glossary

This section provides definitions of key terms used in the MIXIN language specification.

- **Mixin**: The fundamental building block in the MIXIN language. It represents a reusable unit that can contain properties, references, or scalar values. Mixins can be inherited, composed, and combined to form complex data structures and logic.

- **Inheritances**: A mechanism for pointing to another mixin or module. An inheritance is represented as arrays of strings, indicating the path to the target mixin. They support both early and late binding. Inheritance in MIXIN is conflict-free, allowing multiple parent mixins to be combined without error.

- **Property**: A named value within a mixin. Properties are named mixins, containing scalar values (e.g., strings, numbers), inheritances to other mixins, or nested properties. Properties define the internal structure or behavior of a mixin.

- **Scalar Value**: A single, indivisible value within a mixin, such as a string, number, boolean, or null. Scalar values can be merged with other properties in a mixin.

- **Early Binding**: A type of reference resolution where the reference is resolved at the time of mixin definition. The reference remains fixed, regardless of changes in inheritance or context.

- **Late Binding**: A type of reference resolution where the reference is dynamically resolved at the time of mixin evaluation or inheritance. This allows references to adapt to changes in the inheritance hierarchy.

- **Lexical Scope**: The context in which a mixin or property is defined. The lexical scope determines the visibility of mixins and properties within a file, directory, or project.

- **Directory Scope**: The scope defined by a directory. All mixins within a directory are part of the directory scope, and files within the directory can reference each other using the directory scope.

- **Cross-File Reference**: A reference that points to a mixin defined in a different file. The reference format includes the file name and mixin name, and MIXIN will automatically search for the target mixin within the directory hierarchy.

- **Schema**: A JSON Schema definition that describes the structure of a MIXIN file. The schema defines the types, constraints, and relationships between mixins, properties, and references.

- **File Format**: The supported formats for defining MIXIN source code. MIXIN supports YAML, JSON, and TOML, with restrictions to ensure compatibility with JSON serialization.

- **Naming Convention**: The rules for naming mixins and files in the MIXIN language. These conventions help distinguish between type-like mixins, value-like mixins, and instances, and ensure clarity and consistency in code organization.
