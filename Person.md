# Person Entity Schema Research & Standards

## Overview
This document consolidates research on standardizing Person entity schemas across different standards, systems, and vendors. The goal is to understand how to assemble and organize information for an approximate solution to the common problem of schema fragmentation.

## Goals & Objectives
- **Standardization**: Create unified Person entity schemas that bridge different standards
- **Interoperability**: Enable seamless data exchange between systems
- **Reduced Fragmentation**: Minimize duplicate schema definitions across projects
- **Vendor Compatibility**: Maintain compatibility with major platform implementations
- **Extensibility**: Support domain-specific requirements while preserving core structure

## Evaluation Criteria for Schema Organization

### 1. Interoperability
- **Standard Compliance**: Adherence to established industry standards
- **Vendor Compatibility**: Alignment with major platform schemas
- **API Integration**: Ease of integration with existing systems

### 2. Extensibility
- **Custom Fields**: Support for domain-specific requirements
- **Versioning**: Backward compatibility and evolution paths
- **Modularity**: Independent entity definitions with clear relationships

### 3. Data Quality
- **Validation Rules**: Built-in data integrity constraints
- **Required vs Optional**: Clear field requirements
- **Data Types**: Appropriate primitive and complex types

### 4. Business Logic
- **Domain Alignment**: Reflects real-world business relationships
- **Workflow Support**: Enables common business processes
- **Audit Trail**: Change tracking and history

### 5. Performance & Scalability
- **Query Efficiency**: Optimized for common access patterns
- **Storage Optimization**: Efficient data representation
- **Indexing Strategy**: Support for fast lookups

## Sources of Guidance

### International Standards Organizations
- **ISO (International Organization for Standardization)**
- **UN/CEFACT (United Nations Centre for Trade Facilitation and Electronic Business)**
- **W3C (World Wide Web Consortium)**
- **IEEE (Institute of Electrical and Electronics Engineers)**

### Industry-Specific Standards
- **FIBO (Financial Industry Business Ontology)**
- **ACORD (Association for Cooperative Operations Research and Development)**
- **HL7 FHIR (Health Level 7 Fast Healthcare Interoperability Resources)**
- **OAGIS (Open Applications Group Integration Specification)**

### Product Classification Standards
- **UNSPSC (United Nations Standard Products and Services Code)**
- **eCl@ss (International Product Classification)**
- **ETIM (Technical Product Information Models)**
- **GS1 (Global Standards for Business Communication)**

### Major Technology Vendors
- **Salesforce** - CRM Platform
- **HubSpot** - Marketing & CRM Platform
- **Shopify** - E-commerce Platform
- **Microsoft** - Dynamics 365 & Graph API
- **AWS** - Cloud Services
- **Oracle** - Database & ERP
- **SAP** - Enterprise Resource Planning
- **IBM** - Integration & Analytics

### Open Source & Community Standards
- **Schema.org** - Web markup schemas
- **GraphQL** - API query language
- **OpenAPI/Swagger** - API specification
- **JSON Schema** - Data validation

### Development Frameworks
- **Prisma** - Database toolkit
- **TypeORM** - Object-relational mapping
- **TOGAF** - Enterprise architecture

## Schema Examples by Category

### 1. International Standards

#### ISO 20022 - Financial Messaging
```json
{
  "Person": {
    "id": "string",
    "given_name": "string",
    "family_name": "string",
    "birth_date": "date",
    "nationality": "string",
    "identification": {
      "type": "enum(passport, national_id, tax_id, ssn)",
      "number": "string",
      "issuing_country": "string"
    },
    "contact": {
      "email": "string",
      "phone": "string",
      "address": {
        "street": "string",
        "city": "string",
        "postal_code": "string",
        "country": "string"
      }
    },
    "employment": {
      "employer": "string",
      "job_title": "string",
      "employee_id": "string"
    },
    "financial": {
      "tax_id": "string",
      "bank_accounts": "array<object>",
      "credit_score": "integer"
    }
  }
}
```

#### UN/CEFACT - Trade Facilitation
```json
{
  "Person": {
    "id": "string",
    "name": {
      "given_name": "string",
      "family_name": "string",
      "middle_name": "string",
      "title": "enum(mr, mrs, ms, dr, prof)"
    },
    "birth": {
      "date": "date",
      "place": "string",
      "country": "string"
    },
    "nationality": "string",
    "identification": {
      "passport": "string",
      "national_id": "string",
      "tax_number": "string"
    },
    "contact": {
      "email": "string",
      "phone": "string",
      "address": "object"
    },
    "occupation": "string",
    "employer": "string"
  }
}
```

#### ISO 6523 - Organization Identifiers
```json
{
  "Person": {
    "id": "string",
    "organization_identifier": {
      "scheme": "enum(duns, lei, bic, isin, cusip)",
      "value": "string",
      "issuing_organization": "string"
    },
    "name": {
      "given_name": "string",
      "family_name": "string",
      "legal_name": "string"
    },
    "role": "enum(owner, director, officer, employee, contractor)",
    "identification": {
      "passport": "string",
      "national_id": "string",
      "tax_id": "string"
    },
    "contact": {
      "email": "string",
      "phone": "string",
      "address": "object"
    }
  }
}
```

### 2. Industry-Specific Standards

#### FIBO (Financial Industry Business Ontology)
```json
{
  "Person": {
    "id": "string",
    "legal_name": "string",
    "date_of_birth": "date",
    "nationality": "string",
    "tax_identification": {
      "type": "enum(ssn, tin, national_id)",
      "number": "string",
      "issuing_country": "string"
    },
    "employment": {
      "employer": "string",
      "job_title": "string",
      "employee_id": "string",
      "start_date": "date"
    },
    "financial_profile": {
      "credit_score": "integer",
      "annual_income": "decimal",
      "net_worth": "decimal",
      "risk_tolerance": "enum(low, medium, high)"
    },
    "contact": {
      "email": "string",
      "phone": "string",
      "address": "object"
    }
  }
}
```

#### ACORD (Insurance Industry)
```json
{
  "Person": {
    "id": "string",
    "name": {
      "first": "string",
      "last": "string",
      "middle": "string",
      "suffix": "string"
    },
    "birth_date": "date",
    "gender": "enum(male, female, other)",
    "marital_status": "enum(single, married, divorced, widowed, separated)",
    "occupation": "string",
    "employer": "string",
    "drivers_license": {
      "number": "string",
      "state": "string",
      "expiration": "date"
    },
    "contact": {
      "email": "string",
      "phone": "string",
      "address": "object"
    },
    "insurance_history": {
      "policies": "array<object>",
      "claims": "array<object>",
      "rating_factors": "array<object>"
    }
  }
}
```

#### HL7 FHIR (Healthcare)
```json
{
  "Person": {
    "resourceType": "Patient",
    "id": "string",
    "identifier": "array<object>",
    "active": "boolean",
    "name": "array<object>",
    "telecom": "array<object>",
    "gender": "enum(male, female, other, unknown)",
    "birthDate": "date",
    "deceasedBoolean": "boolean",
    "deceasedDateTime": "datetime",
    "address": "array<object>",
    "maritalStatus": "object",
    "multipleBirthBoolean": "boolean",
    "multipleBirthInteger": "integer",
    "photo": "array<object>",
    "contact": "array<object>",
    "communication": "array<object>",
    "generalPractitioner": "array<object>",
    "managingOrganization": "object",
    "link": "array<object>"
  }
}
```

### 3. Product Classification Standards

#### UNSPSC (Product Classification)
```json
{
  "Person": {
    "id": "string",
    "name": "string",
    "role": "enum(product_owner, supplier, manufacturer, distributor)",
    "product_categories": "array<string>",
    "certifications": "array<string>",
    "contact": {
      "email": "string",
      "phone": "string",
      "address": "object"
    },
    "business_scope": "array<string>",
    "compliance_status": "enum(certified, pending, expired)"
  }
}
```

#### eCl@ss (Product Classification)
```json
{
  "Person": {
    "id": "string",
    "name": "string",
    "classification_role": "enum(classifier, reviewer, approver, user)",
    "expertise_areas": "array<string>",
    "classification_permissions": "array<string>",
    "contact": {
      "email": "string",
      "phone": "string",
      "organization": "string"
    },
    "certification_level": "enum(basic, intermediate, expert, master)"
  }
}
```

#### ETIM (Technical Product Information)
```json
{
  "Person": {
    "id": "string",
    "name": "string",
    "technical_role": "enum(engineer, technician, specialist, consultant)",
    "technical_domains": "array<string>",
    "certifications": "array<object>",
    "experience_level": "enum(junior, mid, senior, expert)",
    "contact": {
      "email": "string",
      "phone": "string",
      "address": "object"
    },
    "specializations": "array<string>"
  }
}
```

#### GS1 (Product Identification)
```json
{
  "Person": {
    "id": "string",
    "name": "string",
    "gs1_role": "enum(manufacturer, distributor, retailer, consumer)",
    "gs1_member_id": "string",
    "product_relationships": "array<object>",
    "contact": {
      "email": "string",
      "phone": "string",
      "address": "object"
    },
    "gs1_certification": "enum(active, suspended, expired)"
  }
}
```

### 4. Business Process Standards

#### OAGIS (Business Process Standards)
```json
{
  "Person": {
    "id": "string",
    "name": "string",
    "business_role": "enum(process_owner, participant, approver, stakeholder)",
    "process_permissions": "array<string>",
    "workflow_assignments": "array<object>",
    "contact": {
      "email": "string",
      "phone": "string",
      "address": "object"
    },
    "business_unit": "string",
    "process_expertise": "array<string>"
  }
}
```

### 5. Enterprise Architecture Frameworks

#### TOGAF (Enterprise Architecture)
```json
{
  "Person": {
    "id": "string",
    "name": "string",
    "enterprise_role": "enum(architect, stakeholder, decision_maker, user)",
    "architecture_domains": "array<enum(business, data, application, technology)>",
    "stakeholder_concerns": "array<string>",
    "contact": {
      "email": "string",
      "phone": "string",
      "address": "object"
    },
    "architecture_governance": "enum(owner, steward, custodian, user)",
    "business_impact_level": "enum(low, medium, high, critical)"
  }
}
```

### 6. API & Web Standards

#### Schema.org (Web Markup)
```json
{
  "Person": {
    "@type": "Person",
    "@id": "string",
    "name": "string",
    "givenName": "string",
    "familyName": "string",
    "additionalName": "string",
    "honorificPrefix": "string",
    "honorificSuffix": "string",
    "gender": "enum(male, female, other)",
    "birthDate": "date",
    "deathDate": "date",
    "nationality": "string",
    "address": {
      "@type": "PostalAddress",
      "streetAddress": "string",
      "addressLocality": "string",
      "addressRegion": "string",
      "postalCode": "string",
      "addressCountry": "string"
    },
    "telephone": "string",
    "email": "string",
    "url": "string",
    "image": "string",
    "jobTitle": "string",
    "worksFor": "string",
    "alumniOf": "string",
    "knows": "array<string>",
    "relatedTo": "array<string>"
  }
}
```

#### GraphQL (API Schema)
```graphql
type Person {
  id: ID!
  name: String!
  email: String
  phone: String
  address: Address
  role: PersonRole!
  permissions: [Permission!]!
  metadata: PersonMetadata
  createdAt: DateTime!
  updatedAt: DateTime!
}

type Address {
  street: String!
  city: String!
  state: String
  postalCode: String
  country: String!
}

enum PersonRole {
  USER
  ADMIN
  MODERATOR
  GUEST
}

type Permission {
  resource: String!
  action: String!
  scope: String
}

type PersonMetadata {
  tags: [String!]
  preferences: JSON
  settings: JSON
}
```

#### OpenAPI/Swagger (API Specification)
```yaml
components:
  schemas:
    Person:
      type: object
      required:
        - id
        - name
        - email
      properties:
        id:
          type: string
          format: uuid
          description: Unique identifier for the person
        name:
          type: string
          minLength: 1
          maxLength: 100
          description: Full name of the person
        email:
          type: string
          format: email
          description: Email address
        phone:
          type: string
          pattern: '^\+?[1-9]\d{1,14}$'
          description: Phone number in E.164 format
        address:
          $ref: '#/components/schemas/Address'
        role:
          type: string
          enum: [user, admin, moderator, guest]
          default: user
        metadata:
          type: object
          additionalProperties: true
        created_at:
          type: string
          format: date-time
        updated_at:
          type: string
          format: date-time
```

### 7. Database & ORM Frameworks

#### Prisma (Database Schema)
```prisma
model Person {
  id        String   @id @default(cuid())
  email     String   @unique
  name      String
  phone     String?
  role      Role     @default(USER)
  
  // Address
  street    String?
  city      String?
  state     String?
  postalCode String?
  country   String?
  
  // Metadata
  metadata  Json?
  tags      String[]
  
  // Timestamps
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
  
  // Relations
  accounts  Account[]
  orders    Order[]
  
  @@map("persons")
}

enum Role {
  USER
  ADMIN
  MODERATOR
  GUEST
}
```

#### TypeORM (Entity Schema)
```typescript
import { Entity, PrimaryGeneratedColumn, Column, CreateDateColumn, UpdateDateColumn, OneToMany } from "typeorm";
import { Account } from "./Account";
import { Order } from "./Order";

@Entity("persons")
export class Person {
  @PrimaryGeneratedColumn("uuid")
  id: string;

  @Column({ length: 100 })
  name: string;

  @Column({ unique: true })
  email: string;

  @Column({ nullable: true })
  phone: string;

  @Column({
    type: "enum",
    enum: ["user", "admin", "moderator", "guest"],
    default: "user"
  })
  role: string;

  // Address fields
  @Column({ nullable: true })
  street: string;

  @Column({ nullable: true })
  city: string;

  @Column({ nullable: true })
  state: string;

  @Column({ nullable: true })
  postalCode: string;

  @Column({ nullable: true })
  country: string;

  @Column("simple-array", { nullable: true })
  tags: string[];

  @Column("json", { nullable: true })
  metadata: object;

  @CreateDateColumn()
  createdAt: Date;

  @UpdateDateColumn()
  updatedAt: Date;

  @OneToMany(() => Account, account => account.person)
  accounts: Account[];

  @OneToMany(() => Order, order => order.person)
  orders: Order[];
}
```

#### Oracle Database (SQL Schema)
```sql
CREATE TABLE persons (
  person_id NUMBER GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
  first_name VARCHAR2(50) NOT NULL,
  last_name VARCHAR2(50) NOT NULL,
  email VARCHAR2(100) UNIQUE NOT NULL,
  phone VARCHAR2(20),
  
  -- Address
  street_address VARCHAR2(200),
  city VARCHAR2(50),
  state VARCHAR2(50),
  postal_code VARCHAR2(20),
  country VARCHAR2(50),
  
  -- Business
  company VARCHAR2(100),
  job_title VARCHAR2(100),
  department VARCHAR2(100),
  
  -- Metadata
  status VARCHAR2(20) DEFAULT 'ACTIVE',
  created_date TIMESTAMP DEFAULT SYSTIMESTAMP,
  modified_date TIMESTAMP DEFAULT SYSTIMESTAMP,
  
  -- Constraints
  CONSTRAINT chk_status CHECK (status IN ('ACTIVE', 'INACTIVE', 'PENDING'))
);

-- Indexes
CREATE INDEX idx_persons_email ON persons(email);
CREATE INDEX idx_persons_name ON persons(last_name, first_name);
CREATE INDEX idx_persons_company ON persons(company);
```

### 8. Major Vendor Platforms

#### Salesforce (CRM Platform)
```json
{
  "Person": {
    "Id": "string",
    "FirstName": "string",
    "LastName": "string",
    "Salutation": "enum(mr, mrs, ms, dr, prof)",
    "MiddleName": "string",
    "Suffix": "string",
    "Title": "string",
    "Department": "string",
    "Company": "string",
    "Email": "string",
    "Phone": "string",
    "MobilePhone": "string",
    "HomePhone": "string",
    "OtherPhone": "string",
    "MailingAddress": {
      "Street": "string",
      "City": "string",
      "State": "string",
      "PostalCode": "string",
      "Country": "string"
    },
    "OtherAddress": "object",
    "Birthdate": "date",
    "LeadSource": "enum(web, phone, referral, other)",
    "Industry": "string",
    "AnnualRevenue": "decimal",
    "NumberOfEmployees": "integer",
    "Description": "string",
    "CreatedDate": "datetime",
    "LastModifiedDate": "datetime",
    "SystemModstamp": "datetime"
  }
}
```

#### HubSpot (Marketing & CRM)
```json
{
  "Person": {
    "id": "string",
    "properties": {
      "firstname": "string",
      "lastname": "string",
      "email": "string",
      "phone": "string",
      "company": "string",
      "website": "string",
      "jobtitle": "string",
      "address": "string",
      "city": "string",
      "state": "string",
      "zip": "string",
      "country": "string",
      "lifecyclestage": "enum(lead, marketingqualifiedlead, salesqualifiedlead, opportunity, customer, evangelist, other)",
      "lead_status": "enum(new, contacted, qualified, unqualified, open, in_progress, presentationscheduled, contractsent, closedwon, closedlost)",
      "hs_lead_score": "integer",
      "total_revenue": "decimal",
      "num_associated_deals": "integer",
      "createdate": "datetime",
      "lastmodifieddate": "datetime"
    }
  }
}
```

#### Shopify (E-commerce Platform)
```json
{
  "Person": {
    "id": "string",
    "email": "string",
    "accepts_marketing": "boolean",
    "created_at": "datetime",
    "updated_at": "datetime",
    "first_name": "string",
    "last_name": "string",
    "orders_count": "integer",
    "state": "enum(disabled, enabled, invited)",
    "total_spent": "decimal",
    "last_order_id": "string",
    "note": "string",
    "verified_email": "boolean",
    "multipass_identifier": "string",
    "tax_exempt": "boolean",
    "tags": "string",
    "last_order_name": "string",
    "currency": "string",
    "phone": "string",
    "addresses": "array<object>",
    "accepts_marketing_updated_at": "datetime",
    "marketing_opt_in_level": "enum(single_opt_in, double_opt_in, confirmed_opt_in)",
    "tax_exemptions": "array<string>",
    "admin_graphql_api_id": "string",
    "default_address": "object"
  }
}
```

#### Microsoft Dynamics 365 (ERP Platform)
```json
{
  "Person": {
    "contactid": "string",
    "firstname": "string",
    "lastname": "string",
    "middlename": "string",
    "fullname": "string",
    "jobtitle": "string",
    "department": "string",
    "emailaddress1": "string",
    "emailaddress2": "string",
    "emailaddress3": "string",
    "telephone1": "string",
    "telephone2": "string",
    "telephone3": "string",
    "mobilephone": "string",
    "fax": "string",
    "birthdate": "date",
    "gendercode": "enum(male, female, unknown)",
    "maritalstatuscode": "enum(single, married, divorced, widowed, other)",
    "anniversary": "date",
    "childrensnames": "string",
    "spousesname": "string",
    "creditonhold": "boolean",
    "creditlimit": "decimal",
    "creditlimit_base": "decimal",
    "createdon": "datetime",
    "modifiedon": "datetime",
    "statecode": "enum(active, inactive)",
    "statuscode": "enum(active, inactive, inactive_relationship)"
  }
}
```

#### SAP ERP (Enterprise Resource Planning)
```json
{
  "Person": {
    "id": "string",
    "personnel_number": "string",
    "name": {
      "first_name": "string",
      "last_name": "string",
      "middle_name": "string"
    },
    "personal_data": {
      "birth_date": "date",
      "gender": "enum(male, female, other)",
      "marital_status": "enum(single, married, divorced, widowed)",
      "nationality": "string"
    },
    "employment": {
      "employee_group": "string",
      "employee_subgroup": "string",
      "cost_center": "string",
      "company_code": "string",
      "personnel_area": "string",
      "personnel_subarea": "string"
    },
    "contact": {
      "email": "string",
      "phone": "string",
      "address": "object"
    },
    "organizational_assignment": {
      "position": "string",
      "organizational_unit": "string",
      "supervisor": "string"
    }
  }
}
```

#### AWS Service Catalog (Cloud Services)
```json
{
  "Person": {
    "id": "string",
    "name": "string",
    "aws_identity": {
      "user_arn": "string",
      "user_id": "string",
      "account_id": "string"
    },
    "catalog_permissions": {
      "can_provision": "boolean",
      "can_terminate": "boolean",
      "can_update": "boolean",
      "can_tag": "boolean"
    },
    "resource_access": "array<object>",
    "contact": {
      "email": "string",
      "phone": "string"
    },
    "cost_center": "string",
    "department": "string"
  }
}
```

#### IBM Integration (Analytics & Integration)
```json
{
  "Person": {
    "id": "string",
    "name": "string",
    "integration_roles": "array<enum(source_system_owner, target_system_owner, data_steward, integration_developer)>",
    "system_access": "array<object>",
    "data_governance": {
      "data_owner": "boolean",
      "data_steward": "boolean",
      "data_custodian": "boolean"
    },
    "contact": {
      "email": "string",
      "phone": "string",
      "address": "object"
    },
    "integration_permissions": "array<string>",
    "audit_responsibilities": "array<string>"
  }
}
```

### 9. Content & Development Platforms

#### Wikipedia API (Content Platform)
```json
{
  "Person": {
    "id": "string",
    "title": "string",
    "page_id": "integer",
    "revision_id": "integer",
    "timestamp": "datetime",
    "user": {
      "id": "integer",
      "name": "string",
      "edit_count": "integer",
      "registration": "datetime",
      "groups": "array<string>",
      "rights": "array<string>"
    },
    "content": {
      "extract": "string",
      "categories": "array<string>",
      "links": "array<object>",
      "references": "array<object>"
    },
    "metadata": {
      "language": "string",
      "namespace": "integer",
      "protection": "object"
    }
  }
}
```

#### GitHub API (Development Platform)
```json
{
  "Person": {
    "id": "integer",
    "login": "string",
    "node_id": "string",
    "avatar_url": "string",
    "gravatar_id": "string",
    "url": "string",
    "html_url": "string",
    "followers_url": "string",
    "following_url": "string",
    "gists_url": "string",
    "starred_url": "string",
    "subscriptions_url": "string",
    "organizations_url": "string",
    "repos_url": "string",
    "events_url": "string",
    "received_events_url": "string",
    "type": "enum(user, organization)",
    "site_admin": "boolean",
    "name": "string",
    "company": "string",
    "blog": "string",
    "location": "string",
    "email": "string",
    "hireable": "boolean",
    "bio": "string",
    "twitter_username": "string",
    "public_repos": "integer",
    "public_gists": "integer",
    "followers": "integer",
    "following": "integer",
    "created_at": "datetime",
    "updated_at": "datetime"
  }
}
```

## Key Observations & Patterns

### Common Core Fields
All schemas include basic identity fields:
- **Name**: First, last, middle names
- **Contact**: Email, phone, address
- **Identification**: ID, role, status

### Domain Specialization
- **Financial**: Focus on credit, risk, employment
- **Healthcare**: Medical records, insurance, compliance
- **E-commerce**: Purchase behavior, marketing preferences
- **Enterprise**: Organizational structure, permissions
- **Development**: Technical skills, contributions, access rights

### Schema Complexity Levels
1. **Simple**: Basic contact information (e.g., GraphQL, Prisma)
2. **Moderate**: Business logic + contact (e.g., Salesforce, HubSpot)
3. **Complex**: Domain-specific + extensive metadata (e.g., SAP, HL7 FHIR)

## Recommendations for Unified Schema

### Core Person Schema
```json
{
  "Person": {
    "id": "string",
    "name": {
      "first": "string",
      "last": "string",
      "middle": "string",
      "title": "string",
      "suffix": "string"
    },
    "contact": {
      "email": "string",
      "phone": "string",
      "address": "object"
    },
    "metadata": {
      "created_at": "datetime",
      "updated_at": "datetime",
      "source_system": "string",
      "external_ids": "array<object>"
    }
  }
}
```

### Extension Points
- **Industry-specific fields** via metadata objects
- **Vendor compatibility** through external_id mappings
- **Custom validation** via schema extensions
- **Version evolution** through backward-compatible additions

This research provides a foundation for creating interoperable Person entity schemas that can bridge the gap between different standards, frameworks, and vendor implementations.

## PII (Personally Identifiable Information) Analysis

### High-Risk PII (Direct Identifiers)
- **`id`** - Internal system identifiers
- **`passport_number`** - Government-issued travel documents
- **`national_id`** - Government identification numbers
- **`ssn`** - Social Security Numbers (US)
- **`tax_id`** - Tax identification numbers
- **`drivers_license`** - State/provincial license numbers
- **`birth_date`** - Date of birth
- **`birth_place`** - Location of birth
- **`gender`** - Gender identification
- **`photo`** - Personal photographs

### Medium-Risk PII (Quasi-Identifiers)
- **`email`** - Email addresses
- **`phone`** - Phone numbers (mobile, home, work)
- **`address`** - Complete physical addresses
- **`postal_code`** - ZIP/postal codes
- **`name`** - Full names (first, last, middle)
- **`marital_status`** - Relationship status
- **`nationality`** - Citizenship information
- **`occupation`** - Job/profession details

### Lower-Risk PII (Contextual Identifiers)
- **`age`** - Age or age range
- **`city`** - City of residence
- **`state/province`** - State/provincial location
- **`country`** - Country of residence
- **`company`** - Employer organization
- **`department`** - Work department
- **`job_title`** - Professional position
- **`industry`** - Business sector

### PII by Industry Context
- **Financial Services**: Credit scores, annual income, net worth, bank accounts, tax records
- **Healthcare**: Medical record numbers, health insurance IDs, diagnosis information, treatment history
- **E-commerce**: Purchase history, payment methods, shipping addresses, marketing preferences
- **Enterprise**: Employee IDs, organizational hierarchy, access permissions, performance data

### Data Protection Considerations
- **GDPR**: Special category data (health, biometric), personal data (names, contact info)
- **CCPA**: Personal information (names, addresses), sensitive personal information (SSNs, financial)
- **HIPAA**: Protected Health Information (PHI), indirect identifiers (dates, geographic data)

### PII Handling Best Practices
- **Data Minimization**: Collect only necessary PII, use pseudonymization
- **Access Controls**: Role-based access, audit logging, encryption
- **Compliance**: Consent management, right to deletion, breach notification, cross-border restrictions
