# Building Azure OpenAI GPT-4o Chat Integration with Lovable

This guide provides a comprehensive one-shot prompt approach for creating an Azure OpenAI-powered chatbot using Lovable.

## Meta-Prompting Technique

Before going into the specific prompt, here's a powerful meta-prompting technique that can help create detailed prompts for Lovable:

```
You are a world class prompt engineer. You put together very detailed prompts that are concise but detailed enough that I can get my desired output when I ask you for a prompt.
```

This meta-prompt can be used before asking any AI assistant to formulate a prompt for Lovable. It helps to get more thorough and technically precise instructions that Lovable can understand.

## One-Shot Prompt for Azure OpenAI Integration

While Lovable officially supports OpenAI and Anthropic, it's possible to adapt it for Azure OpenAI integration through Supabase Edge Functions. Here's a comprehensive one-shot prompt:

```
Create a full-stack chat application that integrates with Azure OpenAI's GPT-4o model. 

I need the following components:

1. A clean, modern chat interface with:
   - Message history display with user/AI distinction
   - Message input field and send button
   - Loading indicator during API calls
   - Error handling for failed API calls
   - Proper message formatting including markdown and code blocks

2. Backend integration with Azure OpenAI using Supabase Edge Functions:
   - Create a secure Edge Function that accepts:
     - Azure OpenAI API key
     - Azure OpenAI endpoint URL
     - Azure OpenAI deployment name for GPT-4o
     - Message history in the OpenAI chat format
   - The Edge Function should:
     - Properly format requests according to Azure OpenAI's API requirements
     - Include proper error handling
     - Return responses in a consistent format
     - Implement rate limiting and timeout handling

3. Security features:
   - Store Azure OpenAI credentials securely in Supabase secrets
   - Implement proper authentication to protect the chat
   - Add Row-Level Security to ensure users only see their own conversations

4. Additional features:
   - Conversation history persistence in Supabase
   - Ability to start new conversations
   - Option to modify system prompt
   - Clear chat functionality

Connect this to Supabase for backend storage and authentication. I'll provide my Azure OpenAI credentials once the implementation is complete.

For the Edge Function, please adapt the OpenAI integration pattern to work with Azure's endpoints, which require a slightly different URL structure and authentication approach.
```

## Important Implementation Details

When implementing the Azure OpenAI integration, keep these technical details in mind:

### Azure OpenAI API Differences

Azure OpenAI API differs from OpenAI's API in a few key ways:

1. **Endpoint Structure**: Azure OpenAI uses a unique endpoint URL for each deployment
   ```
   https://{your-resource-name}.openai.azure.com/openai/deployments/{deployment-id}/chat/completions?api-version={api-version}
   ```

2. **Authentication**: Azure OpenAI uses an API key in the header as `api-key` rather than `Authorization: Bearer`

3. **API Versions**: Azure requires an explicit API version parameter

### Edge Function Implementation Pattern

The Edge Function should follow this pattern:

```typescript
import { serve } from 'https://deno.land/std@0.168.0/http/server.ts'

const corsHeaders = {
  'Access-Control-Allow-Origin': '*',
  'Access-Control-Allow-Headers': 'authorization, x-client-info, apikey, content-type',
}

serve(async (req) => {
  // Handle CORS preflight requests
  if (req.method === 'OPTIONS') {
    return new Response('ok', { headers: corsHeaders })
  }

  try {
    const { messages, systemPrompt } = await req.json()
    
    // Format messages including system prompt
    const formattedMessages = systemPrompt 
      ? [{ role: 'system', content: systemPrompt }, ...messages] 
      : messages
    
    // Get Azure OpenAI credentials from environment variables
    const azureApiKey = Deno.env.get('AZURE_OPENAI_API_KEY')
    const azureEndpoint = Deno.env.get('AZURE_OPENAI_ENDPOINT')
    const azureDeploymentName = Deno.env.get('AZURE_OPENAI_DEPLOYMENT_NAME')
    const azureApiVersion = '2023-05-15' // Update to latest version
    
    // Construct Azure OpenAI URL
    const url = `${azureEndpoint}/openai/deployments/${azureDeploymentName}/chat/completions?api-version=${azureApiVersion}`
    
    // Call Azure OpenAI API
    const response = await fetch(url, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        'api-key': azureApiKey,
      },
      body: JSON.stringify({
        messages: formattedMessages,
        temperature: 0.7,
        max_tokens: 800,
      }),
    })
    
    if (!response.ok) {
      throw new Error(`Azure OpenAI API error: ${response.status} ${response.statusText}`)
    }
    
    const data = await response.json()
    
    // Return the response
    return new Response(JSON.stringify({ 
      message: data.choices[0].message.content,
      usage: data.usage
    }), {
      headers: { ...corsHeaders, 'Content-Type': 'application/json' },
    })
    
  } catch (error) {
    return new Response(JSON.stringify({ error: error.message }), {
      status: 500,
      headers: { ...corsHeaders, 'Content-Type': 'application/json' },
    })
  }
})
```

## Prompting Approach for Complex Requirements

When using Lovable for complex integrations like this Azure OpenAI chatbot, it's best to:

1. **Start with the core structure** and get the basic chat UI working
2. **Add the Supabase integration** next to handle authentication and data storage
3. **Implement the Edge Function** for the Azure OpenAI API connection
4. **Finalize with refinements** to the UI and user experience

This staged approach works better than trying to build everything at once, especially with API integrations that may have subtle implementation differences.

## Follow-up Prompts

After the initial implementation, you may need these follow-up prompts:

1. For fixing Azure API connection issues:
```
The Edge Function is returning an error when connecting to Azure OpenAI. Update the function to better handle the Azure-specific API format, including the correct URL structure and authentication headers. Also add detailed error logging to help diagnose connection problems.
```

2. For enhancing the chat UI:
```
Improve the chat UI with the following features:
- Message typing indicators
- Syntax highlighting for code blocks
- Ability to copy code blocks with a single click
- Better visual distinction between user and AI messages
- Responsive design for mobile devices
```

3. For adding conversation management:
```
Add a sidebar that shows saved conversations and allows users to:
- Switch between different conversations
- Name/rename conversations
- Delete unwanted conversations
- Start a new conversation
```
