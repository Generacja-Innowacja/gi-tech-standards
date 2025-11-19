# Component

## Convention

1. **Encapsulation:** all types/utils/constants/subcomponents used only in a single component should be placed inside of
it, if they're shared beetwen components then they should be treated as globals

2. **Minimization:** files/directories from the structure should be create only if they're needed

3. **Mirroring:** the structure of the component directories mirrors the real structure of the components

## Structure

```txt
|- [ComponentName]
    |- ComponentName.tsx               # View file 
    |- ComponentName.test.ts           # Unit tests
    |- ComponentName.types.ts          # Component-related tests
    |- ComponentName.constants.ts      # Component-related constants
    |- [utils]                         # Component-related utils/hooks
        |- getSomeData.ts              
        |- getSomeData.test.ts
    |- [SubComponent]                  # Subcomponent directory
    |- [OtherSubComponent]             # Subcomponent directory
```
