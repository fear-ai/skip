# Company Entity Schema Research & Standards

## Overview
This document consolidates research on standardizing Company entity schemas across different standards, systems, and vendors. The goal is to understand how to assemble and organize information for an approximate solution to the common problem of schema fragmentation.

## Goals & Objectives
- **Standardization**: Create unified Company entity schemas that bridge different standards
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
  "Company": {
    "id": "string",
    "legal_name": "string",
    "trading_name": "string",
    "registration_number": "string",
    "tax_identification": {
      "type": "enum(vat, tax_id, ein)",
      "number": "string",
      "issuing_country": "string"
    },
    "incorporation": {
      "date": "date",
      "country": "string",
      "state": "string"
    },
    "address": {
      "street": "string",
      "city": "string",
      "postal_code": "string",
      "country": "string"
    },
    "contact": {
      "email": "string",
      "phone": "string",
      "website": "string"
    },
    "financial": {
      "annual_revenue": "decimal",
      "currency": "string",
      "credit_rating": "string"
    }
  }
}
```

#### UN/CEFACT - Trade Facilitation
```json
{
  "Company": {
    "id": "string",
    "name": "string",
    "legal_status": "enum(incorporated, partnership, sole_proprietorship)",
    "registration": {
      "number": "string",
      "authority": "string",
      "date": "date"
    },
    "address": {
      "street": "string",
      "city": "string",
      "postal_code": "string",
      "country": "string"
    },
    "contact": {
      "email": "string",
      "phone": "string",
      "website": "string"
    },
    "business_type": "string",
    "industry_sector": "string"
  }
}
```

#### ISO 6523 - Organization Identifiers
```json
{
  "Company": {
    "id": "string",
    "organization_identifier": {
      "scheme": "enum(duns, lei, bic, isin, cusip)",
      "value": "string",
      "issuing_organization": "string"
    },
    "legal_name": "string",
    "trading_name": "string",
    "registration_number": "string",
    "incorporation_country": "string",
    "address": "object",
    "contact": "object"
  }
}
```

### 2. Industry-Specific Standards

#### FIBO (Financial Industry Business Ontology)
```json
{
  "Company": {
    "id": "string",
    "legal_name": "string",
    "trading_name": "string",
    "registration": {
      "number": "string",
      "authority": "string",
      "date": "date"
    },
    "financial_profile": {
      "annual_revenue": "decimal",
      "total_assets": "decimal",
      "credit_rating": "string",
      "risk_category": "enum(low, medium, high)"
    },
    "ownership": {
      "structure": "enum(public, private, government)",
      "parent_company": "string",
      "subsidiaries": "array<string>"
    },
    "contact": "object",
    "address": "object"
  }
}
```

#### ACORD (Insurance Industry)
```json
{
  "Company": {
    "id": "string",
    "name": "string",
    "legal_status": "string",
    "registration": "object",
    "insurance_license": {
      "number": "string",
      "state": "string",
      "expiration": "date"
    },
    "business_type": "enum(insurer, broker, agent, reinsurer)",
    "financial_strength": "string",
    "contact": "object",
    "address": "object"
  }
}
```

#### HL7 FHIR (Healthcare)
```json
{
  "Company": {
    "resourceType": "Organization",
    "id": "string",
    "identifier": "array<object>",
    "active": "boolean",
    "type": "array<object>",
    "name": "string",
    "alias": "array<string>",
    "telecom": "array<object>",
    "address": "array<object>",
    "partOf": "object",
    "contact": "array<object>",
    "endpoint": "array<object>"
  }
}
```

### 3. Product Classification Standards

#### UNSPSC (Product Classification)
```json
{
  "Company": {
    "id": "string",
    "name": "string",
    "role": "enum(supplier, manufacturer, distributor, retailer)",
    "product_categories": "array<string>",
    "certifications": "array<string>",
    "business_scope": "array<string>",
    "compliance_status": "enum(certified, pending, expired)",
    "contact": "object",
    "address": "object"
  }
}
```

#### eCl@ss (Product Classification)
```json
{
  "Company": {
    "id": "string",
    "name": "string",
    "classification_role": "enum(classifier, reviewer, approver, user)",
    "expertise_areas": "array<string>",
    "classification_permissions": "array<string>",
    "certification_level": "enum(basic, intermediate, expert, master)",
    "contact": "object",
    "address": "object"
  }
}
```

#### ETIM (Technical Product Information)
```json
{
  "Company": {
    "id": "string",
    "name": "string",
    "technical_role": "enum(manufacturer, supplier, service_provider)",
    "technical_domains": "array<string>",
    "certifications": "array<object>",
    "quality_standards": "array<string>",
    "contact": "object",
    "address": "object"
  }
}
```

#### GS1 (Product Identification)
```json
{
  "Company": {
    "id": "string",
    "name": "string",
    "gs1_role": "enum(manufacturer, distributor, retailer)",
    "gs1_member_id": "string",
    "product_relationships": "array<object>",
    "gs1_certification": "enum(active, suspended, expired)",
    "contact": "object",
    "address": "object"
  }
}
```

### 4. Business Process Standards

#### OAGIS (Business Process Standards)
```json
{
  "Company": {
    "id": "string",
    "name": "string",
    "business_role": "enum(supplier, customer, partner, competitor)",
    "process_permissions": "array<string>",
    "workflow_assignments": "array<object>",
    "business_unit": "string",
    "process_expertise": "array<string>",
    "contact": "object",
    "address": "object"
  }
}
```

### 5. Enterprise Architecture Frameworks

#### TOGAF (Enterprise Architecture)
```json
{
  "Company": {
    "id": "string",
    "name": "string",
    "enterprise_role": "enum(owner, partner, supplier, customer)",
    "architecture_domains": "array<enum(business, data, application, technology)>",
    "stakeholder_concerns": "array<string>",
    "architecture_governance": "enum(owner, steward, custodian, user)",
    "business_impact_level": "enum(low, medium, high, critical)",
    "contact": "object",
    "address": "object"
  }
}
```

### 6. API & Web Standards

#### Schema.org (Web Markup)
```json
{
  "Company": {
    "@type": "Organization",
    "@id": "string",
    "name": "string",
    "alternateName": "string",
    "description": "string",
    "url": "string",
    "logo": "string",
    "sameAs": "array<string>",
    "address": {
      "@type": "PostalAddress",
      "streetAddress": "string",
      "addressLocality": "string",
      "addressRegion": "string",
      "postalCode": "string",
      "addressCountry": "string"
    },
    "contactPoint": "array<object>",
    "foundingDate": "date",
    "foundingLocation": "object",
    "parentOrganization": "object",
    "subOrganization": "array<object>",
    "numberOfEmployees": "object",
    "industry": "string"
  }
}
```

#### GraphQL (API Schema)
```graphql
type Company {
  id: ID!
  name: String!
  legalName: String
  tradingName: String
  registrationNumber: String
  industry: String
  size: CompanySize
  address: Address
  contact: Contact
  financials: Financials
  metadata: CompanyMetadata
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

type Contact {
  email: String
  phone: String
  website: String
}

type Financials {
  annualRevenue: Decimal
  currency: String
  creditRating: String
}

enum CompanySize {
  SMALL
  MEDIUM
  LARGE
  ENTERPRISE
}

type CompanyMetadata {
  tags: [String!]
  customFields: JSON
  externalIds: [ExternalId!]
}
```

#### OpenAPI/Swagger (API Specification)
```yaml
components:
  schemas:
    Company:
      type: object
      required:
        - id
        - name
      properties:
        id:
          type: string
          format: uuid
          description: Unique identifier for the company
        name:
          type: string
          minLength: 1
          maxLength: 200
          description: Company name
        legalName:
          type: string
          description: Legal registered name
        tradingName:
          type: string
          description: Trading/business name
        registrationNumber:
          type: string
          description: Business registration number
        industry:
          type: string
          description: Industry sector
        size:
          type: string
          enum: [small, medium, large, enterprise]
          description: Company size category
        address:
          $ref: '#/components/schemas/Address'
        contact:
          $ref: '#/components/schemas/Contact'
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
model Company {
  id        String   @id @default(cuid())
  name      String
  legalName String?
  tradingName String?
  registrationNumber String?
  industry  String?
  size      CompanySize?
  
  // Address
  street    String?
  city      String?
  state     String?
  postalCode String?
  country   String?
  
  // Contact
  email     String?
  phone     String?
  website   String?
  
  // Financials
  annualRevenue Decimal?
  currency  String?
  creditRating String?
  
  // Metadata
  metadata  Json?
  tags      String[]
  
  // Timestamps
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
  
  // Relations
  employees Employee[]
  products  Product[]
  
  @@map("companies")
}

enum CompanySize {
  SMALL
  MEDIUM
  LARGE
  ENTERPRISE
}
```

#### TypeORM (Entity Schema)
```typescript
import { Entity, PrimaryGeneratedColumn, Column, CreateDateColumn, UpdateDateColumn, OneToMany } from "typeorm";
import { Employee } from "./Employee";
import { Product } from "./Product";

@Entity("companies")
export class Company {
  @PrimaryGeneratedColumn("uuid")
  id: string;

  @Column({ length: 200 })
  name: string;

  @Column({ nullable: true })
  legalName: string;

  @Column({ nullable: true })
  tradingName: string;

  @Column({ nullable: true })
  registrationNumber: string;

  @Column({ nullable: true })
  industry: string;

  @Column({
    type: "enum",
    enum: ["small", "medium", "large", "enterprise"],
    nullable: true
  })
  size: string;

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

  // Contact fields
  @Column({ nullable: true })
  email: string;

  @Column({ nullable: true })
  phone: string;

  @Column({ nullable: true })
  website: string;

  // Financial fields
  @Column("decimal", { precision: 15, scale: 2, nullable: true })
  annualRevenue: number;

  @Column({ nullable: true })
  currency: string;

  @Column({ nullable: true })
  creditRating: string;

  @Column("simple-array", { nullable: true })
  tags: string[];

  @Column("json", { nullable: true })
  metadata: object;

  @CreateDateColumn()
  createdAt: Date;

  @UpdateDateColumn()
  updatedAt: Date;

  @OneToMany(() => Employee, employee => employee.company)
  employees: Employee[];

  @OneToMany(() => Product, product => product.company)
  products: Product[];
}
```

#### Oracle Database (SQL Schema)
```sql
CREATE TABLE companies (
  company_id NUMBER GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
  name VARCHAR2(200) NOT NULL,
  legal_name VARCHAR2(200),
  trading_name VARCHAR2(200),
  registration_number VARCHAR2(100),
  industry VARCHAR2(100),
  size VARCHAR2(20),
  
  -- Address
  street_address VARCHAR2(200),
  city VARCHAR2(100),
  state VARCHAR2(100),
  postal_code VARCHAR2(20),
  country VARCHAR2(100),
  
  -- Contact
  email VARCHAR2(100),
  phone VARCHAR2(20),
  website VARCHAR2(200),
  
  -- Financials
  annual_revenue NUMBER(15,2),
  currency VARCHAR2(3),
  credit_rating VARCHAR2(10),
  
  -- Metadata
  status VARCHAR2(20) DEFAULT 'ACTIVE',
  created_date TIMESTAMP DEFAULT SYSTIMESTAMP,
  modified_date TIMESTAMP DEFAULT SYSTIMESTAMP,
  
  -- Constraints
  CONSTRAINT chk_size CHECK (size IN ('small', 'medium', 'large', 'enterprise')),
  CONSTRAINT chk_status CHECK (status IN ('ACTIVE', 'INACTIVE', 'PENDING'))
);

-- Indexes
CREATE INDEX idx_companies_name ON companies(name);
CREATE INDEX idx_companies_industry ON companies(industry);
CREATE INDEX idx_companies_registration ON companies(registration_number);
```

### 8. Major Vendor Platforms

#### Salesforce (CRM Platform)
```json
{
  "Company": {
    "Id": "string",
    "Name": "string",
    "Type": "enum(customer, prospect, partner, competitor, other)",
    "Industry": "string",
    "AnnualRevenue": "decimal",
    "NumberOfEmployees": "integer",
    "Description": "string",
    "BillingAddress": {
      "Street": "string",
      "City": "string",
      "State": "string",
      "PostalCode": "string",
      "Country": "string"
    },
    "ShippingAddress": "object",
    "Phone": "string",
    "Fax": "string",
    "Website": "string",
    "TickerSymbol": "string",
    "Ownership": "enum(private, public, subsidiary, other)",
    "Rating": "enum(hot, warm, cold)",
    "CustomerPriority__c": "string",
    "SLA__c": "string",
    "Active__c": "string",
    "NumberofLocations__c": "integer",
    "UpsellOpportunity__c": "string",
    "SLAExpirationDate__c": "date",
    "SLASerialNumber__c": "string",
    "CreatedDate": "datetime",
    "LastModifiedDate": "datetime",
    "SystemModstamp": "datetime"
  }
}
```

#### HubSpot (Marketing & CRM)
```json
{
  "Company": {
    "id": "string",
    "properties": {
      "name": "string",
      "domain": "string",
      "industry": "string",
      "description": "string",
      "phone": "string",
      "address": "string",
      "city": "string",
      "state": "string",
      "zip": "string",
      "country": "string",
      "numberofemployees": "integer",
      "annualrevenue": "decimal",
      "lifecyclestage": "enum(lead, marketingqualifiedlead, salesqualifiedlead, opportunity, customer, evangelist, other)",
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
  "Company": {
    "id": "string",
    "name": "string",
    "domain": "string",
    "email": "string",
    "phone": "string",
    "address1": "string",
    "address2": "string",
    "city": "string",
    "province": "string",
    "zip": "string",
    "country": "string",
    "country_code": "string",
    "currency": "string",
    "timezone": "string",
    "iana_timezone": "string",
    "shop_owner": "string",
    "money_format": "string",
    "money_with_currency_format": "string",
    "weight_unit": "string",
    "province_code": "string",
    "taxes_included": "boolean",
    "auto_configure_tax_inclusivity": "boolean",
    "tax_shipping": "boolean",
    "county_taxes": "boolean",
    "plan_display_name": "string",
    "plan_name": "string",
    "has_discounts": "boolean",
    "has_gift_cards": "boolean",
    "myshopify_domain": "string",
    "google_apps_domain": "string",
    "google_apps_login_enabled": "boolean",
    "money_in_emails_format": "string",
    "eligible_for_payments": "boolean",
    "requires_extra_payments_agreement": "boolean",
    "password_enabled": "boolean",
    "has_storefront": "boolean",
    "finances": "boolean",
    "primary_location_id": "string",
    "cookie_consent_level": "string",
    "visitor_tracking_consent_preference": "string",
    "checkout_api_supported": "boolean",
    "multi_location_enabled": "boolean",
    "setup_required": "boolean",
    "pre_launch_enabled": "boolean",
    "enabled_presentment_currencies": "array<string>",
    "transactional_sms_disabled": "boolean",
    "marketing_sms_consent_enabled_at_checkout": "boolean",
    "created_at": "datetime",
    "updated_at": "datetime"
  }
}
```

#### Microsoft Dynamics 365 (ERP Platform)
```json
{
  "Company": {
    "accountid": "string",
    "name": "string",
    "accountnumber": "string",
    "revenue": "decimal",
    "revenue_base": "decimal",
    "numberofemployees": "integer",
    "description": "string",
    "address1_name": "string",
    "address1_line1": "string",
    "address1_line2": "string",
    "address1_line3": "string",
    "address1_city": "string",
    "address1_stateorprovince": "string",
    "address1_postalcode": "string",
    "address1_country": "string",
    "address1_telephone1": "string",
    "address1_telephone2": "string",
    "address1_telephone3": "string",
    "address1_fax": "string",
    "address1_latitude": "decimal",
    "address1_longitude": "decimal",
    "telephone1": "string",
    "telephone2": "string",
    "telephone3": "string",
    "fax": "string",
    "websiteurl": "string",
    "emailaddress1": "string",
    "emailaddress2": "string",
    "emailaddress3": "string",
    "industrycode": "enum(accounting, agriculture, automotive, chemical, construction, consulting, education, electronics, energy, entertainment, financial, food, government, healthcare, hospitality, insurance, legal, manufacturing, media, mining, nonprofit, real_estate, retail, service, technology, telecommunications, transportation, utilities, other)",
    "accountcategorycode": "enum(customer, prospect, partner, vendor, competitor, reseller, influencer, press, other)",
    "accountratingcode": "enum(hot, warm, cold)",
    "customertypecode": "enum(competitor, consultant, customer, investor, partner, influencer, press, prospect, reseller, supplier, vendor, other),
    "ownershipcode": "enum(public, private, subsidiary, other)",
    "territorycode": "string",
    "creditonhold": "boolean",
    "creditlimit": "decimal",
    "creditlimit_base": "decimal",
    "createdon": "datetime",
    "modifiedon": "datetime",
    "statecode": "enum(active, inactive)",
    "statuscode": "enum(active, inactive)"
  }
}
```

#### SAP ERP (Enterprise Resource Planning)
```json
{
  "Company": {
    "id": "string",
    "company_code": "string",
    "name": "string",
    "legal_name": "string",
    "trading_name": "string",
    "registration_number": "string",
    "tax_number": "string",
    "vat_number": "string",
    "incorporation_date": "date",
    "country": "string",
    "region": "string",
    "city": "string",
    "postal_code": "string",
    "street": "string",
    "house_number": "string",
    "phone": "string",
    "fax": "string",
    "email": "string",
    "website": "string",
    "industry": "string",
    "business_type": "enum(public, private, government, nonprofit)",
    "currency": "string",
    "language": "string",
    "time_zone": "string",
    "fiscal_year_variant": "string",
    "chart_of_accounts": "string",
    "company_status": "enum(active, inactive, liquidated, merged)"
  }
}
```

#### AWS Service Catalog (Cloud Services)
```json
{
  "Company": {
    "id": "string",
    "name": "string",
    "aws_account_id": "string",
    "organization_id": "string",
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
    "department": "string",
    "business_unit": "string"
  }
}
```

#### IBM Integration (Analytics & Integration)
```json
{
  "Company": {
    "id": "string",
    "name": "string",
    "integration_roles": "array<enum(source_system_owner, target_system_owner, data_steward, integration_developer)>",
    "system_access": "array<object>",
    "data_governance": {
      "data_owner": "boolean",
      "data_steward": "boolean",
      "data_custodian": "boolean"
    },
    "contact": "object",
    "integration_permissions": "array<string>",
    "audit_responsibilities": "array<string>"
  }
}
```

### 9. Content & Development Platforms

#### Wikipedia API (Content Platform)
```json
{
  "Company": {
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
  "Company": {
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
- **Name**: Legal name, trading name, display name
- **Contact**: Email, phone, website
- **Address**: Physical location information
- **Identification**: Registration numbers, tax IDs

### Domain Specialization
- **Financial**: Focus on credit ratings, revenue, risk assessment
- **Healthcare**: Medical organization types, licensing, compliance
- **E-commerce**: Store information, payment processing, shipping
- **Enterprise**: Organizational structure, permissions, cost centers
- **Development**: Repository access, collaboration, contribution tracking

### Schema Complexity Levels
1. **Simple**: Basic company information (e.g., GraphQL, Prisma)
2. **Moderate**: Business logic + company details (e.g., Salesforce, HubSpot)
3. **Complex**: Domain-specific + extensive metadata (e.g., SAP, HL7 FHIR)

## Recommendations for Unified Schema

### Core Company Schema
```json
{
  "Company": {
    "id": "string",
    "name": {
      "legal": "string",
      "trading": "string",
      "display": "string"
    },
    "contact": {
      "email": "string",
      "phone": "string",
      "website": "string"
    },
    "address": "object",
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

This research provides a foundation for creating interoperable Company entity schemas that can bridge the gap between different standards, frameworks, and vendor implementations.
