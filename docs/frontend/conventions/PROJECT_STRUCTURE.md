# Project structure

## Convention

- the domain code should be separated from the global code
- all reusable code should be easily accessible
- API clients should be encapsulated

## Structure

```txt
|- public                               # Non-functional static assets (thumbnail, favicon etc.)
|- e2e
    |- [domain-name]                    # E2E domain
        |- path-name.spec.ts            # Path E2E test
|- src
    |- pages                            # Pages components directory
    |- components                       # React components
        |- shared                       # Components shared/reusable across domains
            |- [ComponentName]          # Individual shared component
        |- [domain-name]                # Domain-specific components (eg. home, admin)
            |- [ComponentName]          # Individual domain component
            |- [OtherComponent]         # Individual domain component
    |- services                         # API clients
        |- [api-name]                   # Individual API client directory (eg.: api, cms)
            |- [schemas]                # Data entries schema models
            |- [client]                 # Client's config
            |- [utils]                  # Client's utils
    |- constants                        # Constants domains
        |- domain-name.ts               # Individual constants domains (eg.: common, user, config, quiz)
    |- types                            # Global types
        |- domain-name.ts               # Individual types domains (eg.: common, user, config, quiz)
    |- utils                            # Global utils domains
        |- [domain-name]                # Single utils domain (eg.: number, text, object)
            |- transformNumber.ts              
            |- transformNumber.test.ts
    |- assets                           # Static assets
        |- icons                        # Vector/icons files (SVG)
        |- images                       # Image files (JPG, PNG, etc.)
```
