# Create an AI Smart Assistant

## Overview

I created an intelligent AI assistant using Amazon Bedrock that leverages knowledge bases and Lambda functions to provide benefits information and process expense submissions. By configuring a Bedrock agent, attaching a pre-existing knowledge base, and integrating it with a Lambda action group, I built a multi-service solution that demonstrates how to combine Bedrock's foundation models with custom business logic for real-world automation.

## Topics Covered

- Created and configured an Amazon Bedrock agent from scratch
- Attached an existing knowledge base to enable intelligent question answering
- Designed and implemented action groups to invoke Lambda functions
- Tested agent functionality across multiple interaction patterns
- Integrated foundation models with serverless compute for dynamic request processing

## Introducing the Technologies

**Amazon Bedrock** is a fully managed service that provides access to foundation models (FMs) from leading AI companies through a single API. Bedrock enables you to build generative AI applications without managing infrastructure—models handle natural language understanding and generation while you focus on application logic.

**Bedrock Agents** extend foundation models by enabling them to take actions. An agent can reason about a user's request, retrieve information from knowledge bases, invoke Lambda functions, and respond intelligently. This allows you to build autonomous AI assistants that go beyond simple text generation.

**Bedrock Knowledge Bases** provide retrieval-augmented generation (RAG) capabilities, allowing agents to ground their responses in your organization's specific documents and data rather than relying only on the model's training data.

**AWS Lambda** serves as the compute backbone for custom business logic. By creating action groups that invoke Lambda functions, I enabled the agent to perform operations like submitting benefit claims, which the foundation model alone cannot do.

| Technology | Purpose |
|---|---|
| Amazon Bedrock | Managed access to foundation models |
| Bedrock Agent | Orchestrates reasoning, knowledge retrieval, and Lambda invocations |
| Bedrock Knowledge Base | Provides RAG for domain-specific information (benefits data) |
| AWS Lambda | Executes custom business logic (expense submission) |
| Action Group | Links agent to Lambda function via OpenAPI schema |

## Tasks

### Task 1: Create a New Amazon Bedrock Agent

I navigated to the Amazon Bedrock console and created a new agent with the following configuration:

1. I clicked **Agents** in the left navigation menu
2. I selected **Create agent** to start the agent setup wizard
3. I entered the following details:
   - **Agent name**: `BenefitsAssistant`
   - **Agent description**: `AI assistant for answering benefits questions and processing expense submissions`
   - **Model**: Selected the Claude model available in my region (Anthropic Claude Instant or Claude 3 depending on availability)
   - **Agent role**: Created a new IAM role with permissions for Bedrock and Lambda invocation

4. I left the optional instructions field blank at this stage and proceeded to complete the agent creation

📝 Note: The agent was created in draft status. I would move it to active status only after attaching the knowledge base and testing functionality.

### Task 2: Attach the Existing Knowledge Base

My knowledge base was pre-existing from an earlier lab setup, containing documentation about company benefits programs.

📝 Note: The Bedrock Knowledge Base was a pre-existing resource created in a previous lab with indexed benefits documentation, selected here to enable the agent to answer questions grounded in that data.

I attached the knowledge base to the agent:

1. From the agent configuration page, I navigated to the **Knowledge bases** section
2. I clicked **Add knowledge base** or **Associate knowledge base**
3. I selected the existing knowledge base from the dropdown list
4. I confirmed the attachment and verified that the knowledge base status showed as active

**Result**: The agent now had access to retrieve information from the knowledge base when answering user questions about benefits.

### Task 3: Create an Action Group and Attach the Lambda Function

I created an action group to enable the agent to submit expense claims by invoking a Lambda function.

#### Step 3.1: Create the Action Group

1. From the agent configuration page, I navigated to the **Action groups** section
2. I clicked **Create action group**
3. I entered the action group name: `SubmitBenefitsAction`
4. I selected **Define with API schemas** as the method for specifying the action
5. I provided a description: `Submits benefit expense claims for processing`

#### Step 3.2: Define the OpenAPI Schema

The action group required an OpenAPI schema to describe the Lambda function interface. I created the following schema:

```json
{
  "openapi": "3.0.0",
  "info": {
    "title": "Benefits Submission API",
    "version": "1.0.0",
    "description": "API for submitting benefit expense claims"
  },
  "paths": {
    "/submit-benefits": {
      "post": {
        "summary": "Submit a benefit expense claim",
        "description": "Submits a new benefit expense claim for processing",
        "operationId": "submitBenefitsClaim",
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "properties": {
                  "employeeId": {
                    "type": "string",
                    "description": "Employee identifier"
                  },
                  "claimType": {
                    "type": "string",
                    "description": "Type of benefit claim (e.g., medical, dental, vision)"
                  },
                  "amount": {
                    "type": "number",
                    "description": "Claim amount in dollars"
                  },
                  "description": {
                    "type": "string",
                    "description": "Details of the expense"
                  }
                },
                "required": ["employeeId", "claimType", "amount"]
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "Claim submitted successfully",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "claimId": {
                      "type": "string",
                      "description": "Unique identifier for the submitted claim"
                    },
                    "status": {
                      "type": "string",
                      "description": "Status of the claim (e.g., pending, approved)"
                    },
                    "message": {
                      "type": "string",
                      "description": "Confirmation message"
                    }
                  }
                }
              }
            }
          }
        }
      }
    }
  }
}
```

#### Step 3.3: Connect to the Lambda Function

1. After defining the schema, I selected **Link to Lambda** or **Add Lambda function**
2. I selected the `submit_benefits` Lambda function from the available options
3. I configured the Lambda function authorization:
   - **Authorization type**: Selected **IAM** (the agent's role would invoke the function)
4. I verified the connection and saved the action group

⚠️ Caution: The agent's IAM role must have `lambda:InvokeFunction` permissions targeting the specific Lambda function ARN. I ensured this permission was included when creating or updating the agent role.

### Task 4: Test the Agent Functionality

I tested the agent to verify both knowledge base retrieval and Lambda invocation capabilities.

#### Test 1: Benefits Question

I navigated to the agent test console:

1. I clicked **Test agent** or opened the agent chat interface
2. I entered a question about benefits: `"What are the coverage limits for dental benefits?"`
3. I observed the agent:
   - Process my natural language query
   - Retrieve relevant information from the knowledge base
   - Formulate a response based on the knowledge base data
4. I verified the response was accurate and grounded in the knowledge base content

✅ Task complete: Agent successfully retrieved and answered a benefits question using the knowledge base.

#### Test 2: Expense Submission

I tested the agent's ability to invoke the Lambda action group:

1. In the test console, I submitted a claim request: `"I need to submit a dental claim for $150 for a cleaning procedure. My employee ID is EMP12345."`
2. I observed the agent:
   - Understand the claim submission request
   - Extract relevant parameters (employee ID, claim type, amount, description)
   - Invoke the `submit_benefits` Lambda function with the extracted data
   - Process the Lambda response and return a confirmation
3. I verified the response included a claim ID and confirmation message

**Expected Lambda Response**:
```json
{
  "claimId": "CLM-20240325-001",
  "status": "pending",
  "message": "Your benefit claim has been submitted successfully and is pending review."
}
```

✅ Task complete: Agent successfully invoked the Lambda function and processed an expense submission.

#### Test 3: Multi-turn Conversation

I tested the agent's ability to handle follow-up questions:

1. I asked an initial question: `"What medical expenses are covered under my plan?"`
2. After receiving a knowledge base response, I asked a follow-up: `"Can I submit a claim for a recent doctor visit?"`
3. I verified the agent understood the context and guided me through the submission process

✅ Task complete: Agent maintained conversation context and seamlessly transitioned from Q&A to action invocation.

## Conclusion

I successfully completed the AI Smart Assistant lab by:

- ✅ Created a new Bedrock agent configured with a Claude foundation model
- ✅ Attached a pre-existing knowledge base to enable RAG-powered question answering about benefits
- ✅ Designed an OpenAPI schema and created an action group linking the agent to the `submit_benefits` Lambda function
- ✅ Tested agent functionality across three scenarios: knowledge base retrieval, Lambda invocation for claim submission, and multi-turn conversation handling
- ✅ Verified the agent could ground responses in company-specific data while performing custom business logic through serverless functions

This lab demonstrated a complete generative AI workflow: foundation models for natural language understanding, knowledge bases for organizational context, and Lambda integration for actionable business processes.

## Additional Resources

- [Amazon Bedrock Documentation](https://docs.aws.amazon.com/bedrock/)
- [Bedrock Agents User Guide](https://docs.aws.amazon.com/bedrock/latest/userguide/agents.html)
- [Knowledge Base for Amazon Bedrock](https://docs.aws.amazon.com/bedrock/latest/userguide/knowledge-bases.html)
- [Bedrock Agent Action Groups](https://docs.aws.amazon.com/bedrock/latest/userguide/agents-action-groups.html)
- [AWS Lambda Developer Guide](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html)
- [OpenAPI Specification](https://spec.openapis.org/oas/v3.0.0)
