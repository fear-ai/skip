# Intermediate Notation for Schema Representation Design

## Overview
This document researches and proposes an intermediate notation system for schema representation that can bridge the gap between different standards, frameworks, and vendor implementations. The goal is to create a capable and expressive schema representation that supports deterministic conversion to and from existing formats while maintaining semantic clarity and extensibility.

## Research Objectives

### Primary Requirements
- **SHOULD**: Readily support rigorous and deterministic conversion to standards bodies, organizations, key industry vendors, and open source developer project formats
- **COULD**: Provide methods and routines for actual structures and data elements conversions to and from representative storage in existing formats
- **MUST**: Maintain semantic equivalence across conversions
- **MUST**: Support bidirectional transformation without data loss

### Target Formats
- **Standards Bodies**: ISO, UN/CEFACT, W3C, IEEE
- **Industry Standards**: FIBO, ACORD, HL7 FHIR, OAGIS
- **Vendor Systems**: Salesforce, HubSpot, Shopify, Microsoft, SAP, AWS, Oracle, IBM
- **Open Source**: GraphQL, OpenAPI, Prisma, TypeORM, JSON Schema
- **Database**: SQL DDL, NoSQL schemas, ORM mappings

## Evaluation Criteria for Intermediate Notation

### 1. Expressiveness
- **Semantic Richness**: Ability to capture complex business concepts and relationships
- **Constraint Support**: Validation rules, business rules, and data integrity constraints
- **Metadata Handling**: Support for annotations, documentation, and governance information
- **Relationship Modeling**: Complex relationships, inheritance, and composition patterns

### 2. Interoperability
- **Format Coverage**: Support for all major target formats without information loss
- **Bidirectional Conversion**: Lossless round-trip conversion between formats
- **Version Compatibility**: Support for different versions of target formats
- **Extension Handling**: Graceful handling of vendor-specific extensions

### 3. Technical Characteristics
- **Human Readability**: Clear, understandable representation for developers and architects
- **Machine Processability**: Efficient parsing, validation, and transformation
- **Performance**: Fast conversion and minimal overhead
- **Tool Support**: Availability of tools for editing, validation, and transformation

### 4. Maintainability
- **Evolution Support**: Ability to evolve schemas over time
- **Backward Compatibility**: Support for gradual migration paths
- **Documentation**: Self-documenting with embedded metadata
- **Governance**: Support for change management and approval workflows

## Research Findings: Existing Approaches

### 1. Schema.org Approach
**Strengths:**
- Rich semantic modeling with RDF/OWL foundations
- Extensive vocabulary for common business concepts
- Strong community adoption and tooling
- Built-in extensibility through custom properties

**Limitations:**
- Focused on web markup rather than enterprise integration
- Limited support for complex validation rules
- No built-in transformation capabilities
- Weak support for vendor-specific extensions

### 2. JSON Schema with Extensions
**Strengths:**
- Familiar JSON syntax for developers
- Rich validation rule support
- Good tooling ecosystem
- Extensible through custom keywords

**Limitations:**
- Limited semantic modeling capabilities
- No built-in transformation framework
- Weak support for complex relationships
- Vendor-specific extensions require custom tooling

### 3. GraphQL Schema Definition Language
**Strengths:**
- Strong typing system
- Good support for relationships
- Built-in introspection capabilities
- Strong tooling ecosystem

**Limitations:**
- Focused on API design rather than data modeling
- Limited validation rule support
- No built-in transformation capabilities
- Weak support for enterprise metadata

### 4. OpenAPI/Swagger
**Strengths:**
- Comprehensive API specification
- Good validation rule support
- Strong tooling ecosystem
- Extensible through vendor extensions

**Limitations:**
- Focused on API design rather than data modeling
- Limited semantic modeling capabilities
- No built-in transformation framework
- Weak support for complex relationships

### 5. Prisma Schema Language
**Strengths:**
- Strong database modeling capabilities
- Good relationship modeling
- Built-in migration support
- Strong tooling ecosystem

**Limitations:**
- Focused on database modeling
- Limited support for business rules
- No built-in transformation capabilities
- Weak support for enterprise metadata

## Proposed Intermediate Notation Design

### Design Philosophy
The intermediate notation should be **semantic-first**, **format-agnostic**, and **transformation-ready**. It should capture the essential meaning and structure of data models while providing clear pathways to various target formats.

### Core Design Principles

#### 1. Semantic Modeling
- **Entity-Centric**: Focus on business entities and their relationships
- **Attribute Classification**: Clear distinction between core, optional, and extended attributes
- **Relationship Modeling**: Support for complex relationships with cardinality and constraints
- **Business Rules**: Embedded validation rules and business logic

#### 2. Extensibility Framework
- **Core Schema**: Minimal, interoperable core for each entity
- **Extension Points**: Clear mechanisms for adding vendor-specific and industry-specific fields
- **Namespace Management**: Organized approach to custom extensions
- **Version Control**: Support for schema evolution and backward compatibility

#### 3. Transformation Support
- **Target Format Mapping**: Explicit mappings to target formats
- **Conversion Rules**: Clear rules for handling format-specific features
- **Validation Integration**: Support for format-specific validation
- **Error Handling**: Graceful handling of conversion issues

### Proposed Notation Structure

#### Core Schema Definition
```yaml
entity: Person
version: "1.0"
description: "Core Person entity for cross-platform interoperability"
namespace: "core"

# Core attributes (present in 80%+ of implementations)
core:
  id:
    type: identifier
    description: "Unique identifier for the person"
    constraints:
      required: true
      unique: true
  
  name:
    type: composite
    description: "Person's name information"
    fields:
      first:
        type: string
        constraints:
          required: true
          max_length: 100
      last:
        type: string
        constraints:
          required: true
          max_length: 100
      middle:
        type: string
        constraints:
          max_length: 100
      title:
        type: string
        constraints:
          max_length: 50
      suffix:
        type: string
        constraints:
          max_length: 50

# Standard attributes (present in 50-80% of implementations)
standard:
  contact:
    type: composite
    description: "Contact information"
    fields:
      email:
        type: email
        constraints:
          max_length: 255
      phone:
        type: phone
        constraints:
          max_length: 20
      address:
        type: reference
        target: Address
        constraints:
          max_occurrences: 5

# Extended attributes (vendor/industry specific)
extensions:
  vendor:
    salesforce:
      Salutation:
        type: enum
        values: [mr, mrs, ms, dr, prof]
        description: "Salesforce salutation field"
      LeadSource:
        type: enum
        values: [web, phone, referral, other]
        description: "Salesforce lead source"
    
    hubspot:
      lifecyclestage:
        type: enum
        values: [lead, marketingqualifiedlead, salesqualifiedlead, opportunity, customer, evangelist, other]
        description: "HubSpot lifecycle stage"
      hs_lead_score:
        type: integer
        constraints:
          min_value: 0
          max_value: 100
        description: "HubSpot lead score"

  industry:
    financial:
      credit_score:
        type: integer
        constraints:
          min_value: 300
          max_value: 850
        description: "FICO credit score"
      annual_income:
        type: decimal
        constraints:
          precision: 15
          scale: 2
        description: "Annual income in base currency"
    
    healthcare:
      medical_record_number:
        type: string
        constraints:
          max_length: 50
        description: "Medical record identifier"
      insurance_provider:
        type: reference
        target: Company
        description: "Health insurance provider"

# Relationships
relationships:
  employer:
    type: reference
    target: Company
    cardinality: "0..1"
    description: "Current employer"
  
  accounts:
    type: reference
    target: Account
    cardinality: "0..*"
    description: "Associated accounts"

# Validation rules
validation:
  - rule: "email_or_phone_required"
    condition: "At least one contact method must be provided"
    expression: "contact.email != null OR contact.phone != null"
  
  - rule: "age_validation"
    condition: "Age must be reasonable if birth date provided"
    expression: "birth_date == null OR (current_date - birth_date) < 150_years"

# Metadata
metadata:
  pii_classification:
    high_risk: [id, birth_date, ssn, passport_number]
    medium_risk: [email, phone, address, name]
    low_risk: [company, job_title, industry]
  
  compliance:
    gdpr: "Supports right to deletion and data portability"
    ccpa: "Supports consumer rights and data disclosure"
    hipaa: "Supports healthcare privacy requirements"
  
  created: "2024-01-01"
  updated: "2024-01-01"
  author: "Schema Standardization Team"
```

#### Company Entity Schema
```yaml
entity: Company
version: "1.0"
description: "Core Company entity for cross-platform interoperability"
namespace: "core"

# Core attributes
core:
  id:
    type: identifier
    description: "Unique identifier for the company"
    constraints:
      required: true
      unique: true
  
  name:
    type: composite
    description: "Company name information"
    fields:
      legal:
        type: string
        constraints:
          required: true
          max_length: 200
        description: "Legal registered name"
      trading:
        type: string
        constraints:
          max_length: 200
        description: "Trading/business name"
      display:
        type: string
        constraints:
          max_length: 200
        description: "Display name for user interfaces"

# Standard attributes
standard:
  contact:
    type: composite
    description: "Contact information"
    fields:
      email:
        type: email
        constraints:
          max_length: 255
      phone:
        type: phone
        constraints:
          max_length: 20
      website:
        type: url
        constraints:
          max_length: 500
  
  address:
    type: composite
    description: "Physical address"
    fields:
      street:
        type: string
        constraints:
          max_length: 200
      city:
        type: string
        constraints:
          max_length: 100
      state:
        type: string
        constraints:
          max_length: 100
      postal_code:
        type: string
        constraints:
          max_length: 20
      country:
        type: string
        constraints:
          max_length: 100

# Extended attributes
extensions:
  vendor:
    salesforce:
      Type:
        type: enum
        values: [customer, prospect, partner, competitor, other]
        description: "Salesforce account type"
      Industry:
        type: string
        constraints:
          max_length: 100
        description: "Salesforce industry field"
      AnnualRevenue:
        type: decimal
        constraints:
          precision: 15
          scale: 2
        description: "Salesforce annual revenue"
    
    hubspot:
      domain:
        type: string
        constraints:
          max_length: 255
        description: "Company domain name"
      numberofemployees:
        type: integer
        constraints:
          min_value: 1
        description: "Number of employees"
      lifecyclestage:
        type: enum
        values: [lead, marketingqualifiedlead, salesqualifiedlead, opportunity, customer, evangelist, other]
        description: "HubSpot lifecycle stage"

  industry:
    financial:
      credit_rating:
        type: string
        constraints:
          max_length: 10
        description: "Credit rating from agencies"
      risk_category:
        type: enum
        values: [low, medium, high]
        description: "Risk assessment category"
    
    insurance:
      insurance_license:
        type: string
        constraints:
          max_length: 50
        description: "Insurance license number"
      financial_strength:
        type: string
        constraints:
          max_length: 50
        description: "Financial strength rating"

# Relationships
relationships:
  employees:
    type: reference
    target: Person
    cardinality: "0..*"
    description: "Company employees"
  
  subsidiaries:
    type: reference
    target: Company
    cardinality: "0..*"
    description: "Subsidiary companies"
  
  parent:
    type: reference
    target: Company
    cardinality: "0..1"
    description: "Parent company"

# Validation rules
validation:
  - rule: "contact_required"
    condition: "At least one contact method must be provided"
    expression: "contact.email != null OR contact.phone != null OR contact.website != null"
  
  - rule: "name_validation"
    condition: "Legal name is required, trading name must differ if provided"
    expression: "name.legal != null AND (name.trading == null OR name.trading != name.legal)"

# Metadata
metadata:
  pii_classification:
    high_risk: [id, tax_id, registration_number]
    medium_risk: [name, address, contact]
    low_risk: [industry, size, description]
  
  compliance:
    gdpr: "Supports data subject rights for company representatives"
    ccpa: "Supports business information disclosure requirements"
    sox: "Supports financial reporting and audit requirements"
  
  created: "2024-01-01"
  updated: "2024-01-01"
  author: "Schema Standardization Team"
```

## Transformation Methods

### 1. Target Format Mapping

#### JSON Schema Transformation
```yaml
transformation:
  target: json_schema
  version: "2020-12"
  
  mapping:
    identifier -> string:
      format: "uuid"
    
    email -> string:
      format: "email"
    
    phone -> string:
      pattern: "^\\+?[1-9]\\d{1,14}$"
    
    url -> string:
      format: "uri"
    
    composite -> object:
      properties: "fields"
      required: "required_fields"
    
    reference -> string:
      format: "uri-reference"
    
    enum -> string:
      enum: "values"
  
  validation:
    required: "core_fields"
    additionalProperties: false
    custom_keywords: "vendor_extensions"
```

#### GraphQL Transformation
```yaml
transformation:
  target: graphql
  version: "2021"
  
  mapping:
    identifier -> ID:
      nonNull: true
    
    string -> String:
      maxLength: "constraints.max_length"
    
    integer -> Int:
      minValue: "constraints.min_value"
      maxValue: "constraints.max_value"
    
    decimal -> Float:
      precision: "constraints.precision"
      scale: "constraints.scale"
    
    composite -> type:
      fields: "fields"
    
    reference -> type:
      target: "target"
    
    enum -> enum:
      values: "values"
  
  output:
    types: "entity_types"
    inputs: "input_types"
    enums: "enum_types"
    interfaces: "interface_types"
```

#### OpenAPI Transformation
```yaml
transformation:
  target: openapi
  version: "3.1.0"
  
  mapping:
    identifier -> string:
      format: "uuid"
      description: "description"
    
    string -> string:
      maxLength: "constraints.max_length"
      minLength: "constraints.min_length"
    
    integer -> integer:
      minimum: "constraints.min_value"
      maximum: "constraints.max_value"
    
    decimal -> number:
      format: "double"
    
    composite -> object:
      properties: "fields"
      required: "required_fields"
    
    reference -> object:
      $ref: "target_reference"
    
    enum -> string:
      enum: "values"
  
  output:
    components:
      schemas: "entity_schemas"
      parameters: "path_parameters"
      responses: "response_schemas"
```

### 2. Vendor-Specific Transformations

#### Salesforce Transformation
```yaml
transformation:
  target: salesforce
  version: "58.0"
  
  mapping:
    identifier -> Id:
      type: "id"
      description: "description"
    
    string -> String:
      length: "constraints.max_length"
      required: "constraints.required"
    
    email -> Email:
      type: "email"
      unique: "constraints.unique"
    
    phone -> Phone:
      type: "phone"
    
    composite -> Custom_Object:
      fields: "fields"
      relationships: "relationships"
    
    enum -> Picklist:
      values: "values"
      multiSelect: false
  
  output:
    objects: "custom_objects"
    fields: "custom_fields"
    validation_rules: "validation_rules"
    triggers: "apex_triggers"
```

#### Prisma Transformation
```yaml
transformation:
  target: prisma
  version: "5.0"
  
  mapping:
    identifier -> String:
      @id
      @default(cuid)
    
    string -> String:
      length: "constraints.max_length"
    
    integer -> Int:
      min: "constraints.min_value"
      max: "constraints.max_value"
    
    decimal -> Decimal:
      precision: "constraints.precision"
      scale: "constraints.scale"
    
    email -> String:
      @unique
      length: "constraints.max_length"
    
    composite -> embedded:
      fields: "fields"
    
    reference -> relation:
      target: "target"
      cardinality: "cardinality"
  
  output:
    models: "prisma_models"
    enums: "prisma_enums"
    relations: "prisma_relations"
```

## Implementation Approach

### 1. Core Components

#### Schema Parser
- **YAML/JSON Parser**: Parse intermediate notation schemas
- **Validation Engine**: Validate schema structure and constraints
- **Semantic Analyzer**: Analyze relationships and dependencies

#### Transformation Engine
- **Format Mappers**: Convert to target formats
- **Validation Integrators**: Integrate format-specific validation
- **Error Handlers**: Handle transformation issues gracefully

#### Code Generators
- **Schema Generators**: Generate target format schemas
- **Validation Code**: Generate validation logic
- **Documentation**: Generate format-specific documentation

### 2. Tooling Ecosystem

#### Development Tools
- **Schema Editor**: Visual editor for intermediate notation
- **Validation Tools**: Real-time validation and error checking
- **Preview Tools**: Preview target format output

#### Integration Tools
- **CI/CD Integration**: Automated schema validation and transformation
- **Version Control**: Track schema changes and versions
- **Collaboration**: Multi-user editing and approval workflows

#### Runtime Tools
- **Validation Runtime**: Runtime validation of data against schemas
- **Transformation Runtime**: Runtime conversion between formats
- **Monitoring**: Track schema usage and performance

### 3. Governance Framework

#### Schema Management
- **Version Control**: Semantic versioning for schemas
- **Change Management**: Approval workflows for schema changes
- **Deprecation**: Graceful deprecation of old schema versions

#### Quality Assurance
- **Validation Testing**: Test schemas against real data
- **Transformation Testing**: Test round-trip conversions
- **Performance Testing**: Test transformation performance

#### Documentation
- **Schema Documentation**: Comprehensive schema documentation
- **Transformation Guides**: Guides for each target format
- **Best Practices**: Implementation best practices

## Demonstration: Person Entity Transformations

### Input: Intermediate Notation (Person)
```yaml
entity: Person
version: "1.0"
core:
  id:
    type: identifier
    required: true
  name:
    type: composite
    fields:
      first: { type: string, required: true, max_length: 100 }
      last: { type: string, required: true, max_length: 100 }
  contact:
    type: composite
    fields:
      email: { type: email, max_length: 255 }
      phone: { type: phone, max_length: 20 }
```

### Output: JSON Schema
```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "title": "Person",
  "type": "object",
  "required": ["id", "name"],
  "properties": {
    "id": {
      "type": "string",
      "format": "uuid",
      "description": "Unique identifier for the person"
    },
    "name": {
      "type": "object",
      "required": ["first", "last"],
      "properties": {
        "first": {
          "type": "string",
          "maxLength": 100,
          "description": "First name"
        },
        "last": {
          "type": "string",
          "maxLength": 100,
          "description": "Last name"
        }
      }
    },
    "contact": {
      "type": "object",
      "properties": {
        "email": {
          "type": "string",
          "format": "email",
          "maxLength": 255,
          "description": "Email address"
        },
        "phone": {
          "type": "string",
          "pattern": "^\\+?[1-9]\\d{1,14}$",
          "maxLength": 20,
          "description": "Phone number"
        }
      }
    }
  },
  "additionalProperties": false
}
```

### Output: GraphQL Schema
```graphql
type Person {
  id: ID!
  name: PersonName!
  contact: PersonContact
}

type PersonName {
  first: String!
  last: String!
}

type PersonContact {
  email: String
  phone: String
}

input CreatePersonInput {
  name: CreatePersonNameInput!
  contact: CreatePersonContactInput
}

input CreatePersonNameInput {
  first: String!
  last: String!
}

input CreatePersonContactInput {
  email: String
  phone: String
}
```

### Output: Prisma Schema
```prisma
model Person {
  id        String   @id @default(cuid())
  name      PersonName
  contact   PersonContact?
  
  @@map("persons")
}

type PersonName {
  first String
  last  String
}

type PersonContact {
  email String?
  phone String?
}
```

## Conclusion

The proposed intermediate notation provides a powerful foundation for schema interoperability across different standards, frameworks, and vendor implementations. By focusing on semantic modeling and providing clear transformation pathways, it enables organizations to maintain single source of truth for data models while supporting multiple target formats.

The key benefits include:
- **Semantic Clarity**: Clear representation of business concepts and relationships
- **Format Independence**: Separation of concerns between modeling and implementation
- **Extensibility**: Support for vendor-specific and industry-specific requirements
- **Transformation Support**: Deterministic conversion to target formats
- **Governance**: Built-in support for schema management and evolution

The next steps involve implementing the transformation engine, building tooling support, and validating the approach with real-world schemas from different domains.

## Appendix: Existing Proposals, Frameworks, and Systems

### 1. Schema.org
- **Purpose**: Web markup schemas for search engines
- **Strengths**: Rich vocabulary, community adoption
- **Limitations**: Web-focused, limited enterprise support

### 2. JSON Schema
- **Purpose**: Data validation and documentation
- **Strengths**: Familiar syntax, good tooling
- **Limitations**: Limited semantic modeling

### 3. GraphQL SDL
- **Purpose**: API schema definition
- **Strengths**: Strong typing, introspection
- **Limitations**: API-focused, limited validation

### 4. OpenAPI/Swagger
- **Purpose**: API specification and documentation
- **Strengths**: Comprehensive API coverage, strong tooling
- **Limitations**: API-focused, limited data modeling

### 5. Prisma Schema Language
- **Purpose**: Database modeling and ORM
- **Strengths**: Database focus, migration support
- **Limitations**: Database-focused, limited business rules

### 6. XML Schema (XSD)
- **Purpose**: XML document validation
- **Strengths**: Mature standard, strong validation
- **Limitations**: XML-specific, complex syntax

### 7. RDF/OWL
- **Purpose**: Semantic web and knowledge representation
- **Strengths**: Rich semantic modeling, logical reasoning
- **Limitations**: Complex, limited tooling

### 8. UML Class Diagrams
- **Purpose**: Software modeling and design
- **Strengths**: Visual representation, standard notation
- **Limitations**: Limited validation, no transformation support

### 9. Entity-Relationship Diagrams
- **Purpose**: Database design and modeling
- **Strengths**: Clear relationship modeling, standard notation
- **Limitations**: Limited business rules, no transformation support

### 10. Business Process Model and Notation (BPMN)
- **Purpose**: Business process modeling
- **Strengths**: Process focus, standard notation
- **Limitations**: Process-focused, limited data modeling

The proposed intermediate notation builds upon these existing approaches while addressing their limitations and providing a unified foundation for cross-platform schema interoperability.
