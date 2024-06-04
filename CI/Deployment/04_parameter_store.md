# 🔐 AWS Parameter Store (Secure Configuration Management)

This section explains how **AWS Systems Manager Parameter Store** is used to securely store sensitive configuration values required by the **AWS CodeBuild buildspec file**, particularly credentials and identifiers for **SonarCloud** integration.

### ❓ Why Parameter Store Is Required

The `buildspec.yml` file is stored in the Git repository and references values such as:

- SonarCloud authentication token
- SonarCloud host URL
- Organization key
- Project key

Storing **actual secret values directly in the repository** is unsafe because:

- Secrets can be accidentally exposed
- Git repositories are often shared or cloned
- Public repositories cannot store secrets at all

To address this, the buildspec file references **parameter names only**, while the real values are securely stored in AWS.

### ✅ Why AWS Parameter Store?

**AWS Systems Manager Parameter Store** is a managed, secure key-value storage service.

#### Advantages

- Free for standard usage
- Supports encrypted values
- Native integration with AWS CodeBuild
- Simple syntax for use in buildspec files

### ⚙️ How Parameter Store Works with CodeBuild

- The buildspec file defines variables under `parameter-store`
- During execution, CodeBuild:

  - Retrieves values from Parameter Store
  - Injects them as environment variables

- Secrets are never committed to Git or exposed in logs (when configured correctly)

### 🧭 Accessing Parameter Store

1. Open the **AWS Console**
2. Search for **Systems Manager**
3. Select **Parameter Store** from the left menu
4. Click **Create parameter**

### 📌 Parameters Required for This Project

Four parameters are created to support SonarCloud integration.

**Parameter 1: Organization**

- **Name:** `ORGANIZATION`
- **Type:** String
- **Value:** SonarCloud organization key
- **Data Type:** Text

**Parameter 2: Host**

- **Name:** `HOST`
- **Type:** String
- **Value:**

  ```text
  https://sonarcloud.io
  ```

- **Data Type:** Text

**Parameter 3: Project**

- **Name:** `PROJECT`
- **Type:** String
- **Value:** SonarCloud project key
- **Data Type:** Text

**Parameter 4: Login (Sonar Token)**

- **Name:** `LOGIN`
- **Type:** SecureString
- **Value:** SonarCloud authentication token
- **Data Type:** Text
- **Encryption:** Enabled (default)

### 🔒 SecureString Usage

- The `LOGIN` parameter is stored as a **SecureString**
- Values are encrypted at rest
- Used by CodeBuild to authenticate with SonarCloud
- Prevents accidental exposure of sensitive tokens

![sonar-parameters](../Resources/Images/sonar-parameters.png)
