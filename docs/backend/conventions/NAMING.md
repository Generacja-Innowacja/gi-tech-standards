# Naming

There are two things hard in programming: cache invalidation and naming things. Organization follows certain rule on
 naming to prevent confusion.

## TypeScript & Nest.js

> **#1. All TypeScript files MUST be named with the `.ts` extension.**

> **#2. File names SHOULD be in lowercase kebab-case.**
>
> Projects should follow the Nest.js convention for file naming, which is widely adopted in the TypeScript community.
>
> In this approach template is defined: `<name>.<type>.ts`, where `<name>` is the name of the resource, and
> `<type>` is the NestJS type suffix. Examples:
>
> - `user.module.ts`
> - `organization.service.ts`
> - `offer.controller.ts`
> - `create-role.request.ts`
> - `survey.model.ts`
>
> Simple files containing only functions MAY be named without the `<type>`, examples:
>
> - `errors.ts`
> - `constants.ts`
> - `utils.ts`
> - `main.ts`

> **#3. Named export MUST be used, default export MUSt NOT be used.**

> **#4. All TypeScript classes, enums, interfaces and types MUST follow the PascalCase naming convention.**
>
> Element name must reflect both the resource and the type, examples:
>
> - `UserModule`
> - `OrganizationService`
> - `OfferController`
> - `CreateRoleRequest`
> - `SurveyModel`

> **#5. All TypeScript consts and functions MUST follow the camelCase naming convention.**
>
> Element name must reflect both the resource and the type, for example:
>
> - `createUser()`
> - `configKey`
> - `token`

> **#6. Directories that group related NestJS artifacts SHOULD use the resource name in kebab-case.**
>
> Directories that group related artifacts with the same type SHOULD be named after the type they represent, in
> lowercase kebab-case. Examples:
>
> - `users/`
> - `orders/`
> - `module/user-role/request`

> **#1. Function SHOULD be written with `function` keyword, arrow functions SHOULD be used only as callbacks.**
>
> ```ts
> // Good
> function createUser(id: string) {}
> 
> // Bad
> const createUser = (id: string) => {}
> 
> // Good
> array.map(item => item.id);
> array.map((item, index) => `${item.id} ${index}`);
> ```

## Cucumber.js

> **#1. Gherkin file MUST be named with the `.feature` extension.**

> **#2. Gherkin file name MUST be in lowercase kebab-case.**
>
> Projects should also follow the Nest.js convention for file naming for gherkin files.
>
> In this approach template is defined: `<action>.<domain>.ts` template for the name, where `<action>` is the action name, and
> `<domain>` is the application domain. Examples:
>
> - `create.user.feature`
> - `revoke-license.organization.feature`
> - `copy.user-role.feature`

> **#3. Scenario names MUST be a sentence, and MUST follow the user story approach.**
>
> User stories are a way to describe the behavior of a system. They are written in plain English and are used to define
> the requirements. They are a way to communicate the intent of the system to the users.
>
> User stories are written in the form of a sentence, examples:
>
> - `As an admin I can remove a user from the organization`
> - `As a user I can create a new organization`
> - `As an admin I cannot update user role for non-existing user`

> **#4. Scenario names MUST NOT be repeated in one test file.**
