# Installation

> `npm install --save types-yeoman-generator`

Change tsconfig compilerOptions

"baseUrl": "./"

"paths": {"yeoman-generator":["types-yeoman-generator"]}

Exclude in .gitignore / npm

## Summary

This package contains type definitions for yeoman-generator <https://github.com/yeoman/generator>.

The original definition file has been extended to allow for:

typed answer when using a single question based upon what is returned from the filter function whose argument is now type any.  The validate function argument is typed appropriately.  If no filter function then the answer defaults to type string.  The single question does not include the answers argument to its function properties.

The Generator is now generic to support typed options as well as the typed answer.

```typescript
interface SingleQuestion<V=string> {
      store?:boolean;
      validate?(input: V): boolean | string | Promise<boolean | string>;
      filter?(input: any): V | Promise<V>;
      //......
}
interface SingleAnswer<V>{
      [key:string]:V
}
declare class Generator<TOptions={}> extends EventEmitter {
    prompt<V>(question: Generator.SingleQuestion<V>): Promise<Generator.SingleAnswer<V>>;
    prompt(questions: Generator.Questions): Promise<Generator.Answers>;
    option<K extends keyof TOptions>(name: K, config: Generator.OptionConfig): this;
    options: TOptions & {[key:string]:any};
    //...additional
}
```

The package depends on inquirer unfortunately its type definition file is not completely accurate.  The filter function should also has the answers as an argument.
