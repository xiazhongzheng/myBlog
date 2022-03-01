Partial，Required，Readonly，Pick，Record，Exclude，Extract，Omit，NonNullable，Parameters，ConstructorParameters，ReturnType，InstanceType，Uppercase，Lowercase，Capitalize，Uncapitalize





```ts
type CapitalizeString<T> = T extends `${infer L}${infer R}` ? `${Uppercase<L>}${R}` : T
```