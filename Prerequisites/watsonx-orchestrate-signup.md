# watsonx Orchestrate Signup and Configuration Guide

Complete guide for signing up for IBM watsonx Orchestrate and configuring your environment for agent development.

## Table of Contents

1. [Overview](#overview)
2. [Sign Up for IBM Cloud](#sign-up-for-ibm-cloud)
3. [Provision watsonx Orchestrate Service](#provision-watsonx-orchestrate-service)
4. [Access watsonx Orchestrate](#access-watsonx-orchestrate)
5. [Generate API Credentials](#generate-api-credentials)
6. [Configure ADK Environment](#configure-adk-environment)
7. [Verify Configuration](#verify-configuration)

---

## Overview

This guide walks you through:

- Creating an IBM Cloud account
- Provisioning a watsonx Orchestrate instance
- Generating API credentials
- Configuring the ADK to connect to your instance

**Estimated Time**: 15-20 minutes

**Prerequisites**:
- ✅ Completed [Environment Setup Guide](environment-setup.md)
- ✅ Valid email address for IBM Cloud account

---

## Sign Up for IBM Cloud

### Step 1: Create IBM Cloud Account

1. **Visit IBM Cloud Registration**
   - Go to [cloud.ibm.com/registration](https://cloud.ibm.com/registration)

2. **Enter Your Information**
   - Email address
   - First and last name
   - Country/Region
   - Password (must meet security requirements)

3. **Accept Terms and Conditions**
   - Review IBM Cloud Terms
   - Check the acceptance box

4. **Complete Registration**
   - Click "Create account"
   - Check your email for verification link
   - Click the verification link to activate your account

5. **Sign In**
   - Go to [cloud.ibm.com](https://cloud.ibm.com)
   - Sign in with your credentials

### Step 2: Verify Account Status

After signing in, you should see the IBM Cloud dashboard. Your account is now ready for service provisioning.

---

## Provision watsonx Orchestrate Service

### Option 1: Free Trial (Recommended for Labs)

1. **Access Free Trial Page**
   - Visit [ibm.com/account/reg/us-en/signup?formid=urx-52753](https://www.ibm.com/account/reg/us-en/signup?formid=urx-52753)
   - Or search for "watsonx Orchestrate free trial" on IBM.com

2. **Start Free Trial**
   - Click "Start your free trial"
   - Sign in with your IBM Cloud account
   - Follow the provisioning wizard

3. **Configure Trial Instance**
   - Select your region (choose closest to your location)
   - Accept trial terms
   - Click "Create"

4. **Wait for Provisioning**
   - Provisioning typically takes 2-5 minutes
   - You'll receive an email when ready

### Option 2: Standard Provisioning (Paid Plan)

1. **Navigate to Catalog**
   - From IBM Cloud dashboard, click "Catalog"
   - Or go to [cloud.ibm.com/catalog](https://cloud.ibm.com/catalog)

2. **Search for watsonx Orchestrate**
   - Type "watsonx Orchestrate" in the search bar
   - Click on "watsonx Orchestrate" service

3. **Configure Service**
   - **Select a region**: Choose your preferred location
   - **Select a pricing plan**: Choose based on your needs
     - Lite (Free tier with limitations)
     - Standard (Pay-as-you-go)
     - Enterprise (Contact IBM)
   - **Service name**: Enter a descriptive name (e.g., "wxo-bobathon-labs")
   - **Resource group**: Select or create a resource group

4. **Create Service**
   - Review your configuration
   - Click "Create"
   - Wait for provisioning to complete

---

## Access watsonx Orchestrate

### Step 1: Locate Your Service Instance

1. **Open IBM Cloud Dashboard**
   - Go to [cloud.ibm.com](https://cloud.ibm.com)
   - Sign in if needed

2. **Navigate to Resource List**
   - Click the hamburger menu (☰) in the top-left
   - Select "Resource list"
   - Or go directly to [cloud.ibm.com/resources](https://cloud.ibm.com/resources)

3. **Find watsonx Orchestrate**
   - Expand "AI / Machine Learning" section
   - Look for your watsonx Orchestrate instance
   - Click on the instance name

### Step 2: Launch watsonx Orchestrate

1. **From the Service Details Page**
   - Click the "Launch watsonx Orchestrate" button
   - A new tab will open with the watsonx Orchestrate interface

2. **First-Time Setup** (if prompted)
   - Complete any initial setup wizards
   - Accept terms of service
   - Configure basic preferences

---

## Generate API Credentials

API credentials are required to connect the ADK to your watsonx Orchestrate instance.

### Step 1: Access API Details

1. **Open watsonx Orchestrate**
   - Launch your watsonx Orchestrate instance (see previous section)

2. **Open Settings**
   - Click your user icon in the top-right corner
   - Select "Settings" from the dropdown menu

3. **Navigate to API Details**
   - Click on the "API details" tab
   - You'll see your service instance URL

### Step 2: Copy Service Instance URL

1. **Locate Service Instance URL**
   - In the API details tab, find the "Service instance URL" field
   - Example format: `https://us-south.ml.cloud.ibm.com/ml/v1/...`

2. **Copy the URL**
   - Click the copy icon next to the URL
   - Or manually select and copy the entire URL
   - **Save this URL** - you'll need it for ADK configuration

### Step 3: Generate API Key

1. **Click "Generate API key" Button**
   - In the API details tab
   - Click the "Generate API key" button

2. **Redirect to IBM Cloud IAM**
   - You'll be redirected to IBM Cloud Identity and Access Management
   - This is the secure way to create API keys

3. **Create API Key**
   - Click "Create" button
   - Enter a descriptive name (e.g., "wxo-adk-bobathon-labs")
   - Add a description (e.g., "API key for ADK development in Bobathon labs")
   - Click "Create"

4. **Copy and Save API Key**
   - **IMPORTANT**: The API key is shown only once
   - Click "Copy" to copy the key
   - **Save it securely** in a password manager or secure note
   - You cannot retrieve this key later
   - If lost, you'll need to generate a new one

### Important Notes About API Keys

⚠️ **Security Best Practices**:
- Never commit API keys to version control
- Don't share API keys in public channels
- Store keys in secure password managers
- Rotate keys periodically
- Delete unused keys

⚠️ **Key Limitations**:
- IBM Cloud accounts: No specific limit
- AWS-hosted instances: Maximum 10 API keys
- Keys cannot be edited or retrieved after creation
- Deleted keys cannot be recovered

---

## Configure ADK Environment

Now configure the ADK to connect to your watsonx Orchestrate instance.

### Step 1: Add Environment to ADK

Open a terminal and run the following command:

#### For IBM Cloud (SaaS)

```bash
orchestrate env add <environment-name> \
  -u <service-instance-url> \
  --type ibm_iam \
  --activate
```

**Replace**:
- `<environment-name>`: Choose a name (e.g., "wxo-prod", "bobathon-labs")
- `<service-instance-url>`: Paste the URL you copied earlier

**Example**:
```bash
orchestrate env add bobathon-labs \
  -u https://us-south.ml.cloud.ibm.com/ml/v1/instances/abc123 \
  --type ibm_iam \
  --activate
```

#### For AWS-Hosted Instances

```bash
orchestrate env add <environment-name> \
  -u <service-instance-url> \
  --type mcsp \
  --activate
```

#### For On-Premises Installations

```bash
orchestrate env add <environment-name> \
  -u <service-instance-url>
```

The ADK will automatically detect the authentication type for on-premises.

### Step 2: Authenticate with API Key

After adding the environment, you'll be prompted to enter your API key:

```
Enter your API key: 
```

**Paste the API key** you generated earlier and press Enter.

**Note**: The key won't be visible as you type (for security).

### Step 3: Verify Environment is Active

```bash
orchestrate env list
```

You should see your environment marked as active (with an asterisk *):

```
* bobathon-labs (ibm_iam)
```

---

## Verify Configuration

### Test 1: Check Environment Connection

```bash
orchestrate env info
```

Expected output:
```
Environment: bobathon-labs
Type: ibm_iam
URL: https://us-south.ml.cloud.ibm.com/ml/v1/instances/abc123
Status: Active
```

### Test 2: List Agents

```bash
orchestrate agent list
```

This should connect to your instance and list any existing agents (may be empty for new instances).

### Test 3: Check ADK Version

```bash
orchestrate --version
```

Ensure you have the latest version installed.

### Test 4: Verify in VS Code

1. **Open VS Code with Bob**
2. **Click the watsonx extension** in the sidebar
3. **Click "Initialize Workspace"**
4. **Verify your environment** appears in the Environment Manager
5. **Click "Activate"** to connect Bob to your environment

---

## Troubleshooting

### Issue: "Invalid API Key"

**Symptoms**: Authentication fails when adding environment

**Solutions**:
1. Verify you copied the complete API key
2. Check for extra spaces or characters
3. Generate a new API key and try again
4. Ensure you're using the API key from watsonx Orchestrate settings, not IBM Cloud resource page

### Issue: "Cannot Connect to Service"

**Symptoms**: ADK can't reach the service instance

**Solutions**:
1. Verify the service instance URL is correct
2. Check your internet connection
3. Ensure the service is provisioned and running
4. Try accessing watsonx Orchestrate in a browser first

### Issue: "Environment Not Found"

**Symptoms**: `orchestrate env list` shows no environments

**Solutions**:
```bash
# Re-add the environment
orchestrate env add <name> -u <url> --type ibm_iam --activate
```

### Issue: "Wrong Authentication Type"

**Symptoms**: Connection fails with authentication error

**Solutions**:
- For IBM Cloud: Use `--type ibm_iam`
- For AWS: Use `--type mcsp`
- For On-premises: Use `--type cpd` or let ADK auto-detect

### Issue: "API Key Limit Reached" (AWS only)

**Symptoms**: Cannot generate new API key

**Solutions**:
1. Delete unused API keys from Settings > API details
2. Contact IBM Support if you need more keys
3. Reuse existing keys if possible

---

## Managing Multiple Environments

You can configure multiple watsonx Orchestrate environments (dev, test, prod):

### Add Additional Environments

```bash
# Add development environment
orchestrate env add wxo-dev -u <dev-url> --type ibm_iam

# Add production environment
orchestrate env add wxo-prod -u <prod-url> --type ibm_iam
```

### Switch Between Environments

```bash
# Activate development
orchestrate env activate wxo-dev

# Activate production
orchestrate env activate wxo-prod

# Check active environment
orchestrate env list
```

### Remove an Environment

```bash
orchestrate env remove <environment-name>
```

---

## Next Steps

✅ **Environment Setup Complete!**

You're now ready to start building agents:

1. 🚀 [Start Lab 2: Build Agentic Workflows](../Lab2%20-%20watsonx%20Orchestrate%20/)
2. 📖 Review [watsonx Orchestrate ADK Documentation](https://developer.watson-orchestrate.ibm.com)
3. 🎓 Explore [IBM Developer Tutorials](https://developer.ibm.com/tutorials/)

---

## Additional Resources

- [watsonx Orchestrate Product Page](https://www.ibm.com/products/watsonx-orchestrate)
- [IBM Cloud Documentation](https://cloud.ibm.com/docs)
- [watsonx Orchestrate Free Trial](https://www.ibm.com/account/reg/us-en/signup?formid=urx-52753)
- [IBM Cloud Support](https://cloud.ibm.com/unifiedsupport/supportcenter)
- [ADK CLI Reference](https://developer.watson-orchestrate.ibm.com/cli/overview)

---

**Need Help?** Contact IBM Support or refer to the [official documentation](https://developer.watson-orchestrate.ibm.com).