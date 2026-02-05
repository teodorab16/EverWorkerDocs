---
title: LLM API failing due to content management policy
fullscreen: false
hidden: false
---
Potential solutions when LLM provider blocks intended request

<br />

# &#x20;Issue description

LLM execution may fail with an error message similar to the one below

```
"error": "LLM API call failed: 400\n{\"error\":{\"message\":\"The response was filtered due to the prompt triggering Azure OpenAI's content management policy. Please modify your prompt and retry. To learn more about our content filtering policies please read our documentation: https://go.microsoft.com/fwlink/?linkid=2198766\",\"type\":null,\"param\":\"prompt\",\"code\":\"content_filter\",\"status\":400,\"innererror\":{\"code\":\"ResponsibleAIPolicyViolation\",\"content_filter_result\":{\"hate\":{\"filtered\":false,\"severity\":\"safe\"},\"jailbreak\":{\"detected\":true,\"filtered\":true},\"self_harm\":{\"filtered\":false,\"severity\":\"safe\"},\"sexual\":{\"filtered\":false,\"severity\":\"safe\"},\"violence\":{\"filtered\":false,\"severity\":\"safe\"}}}}}"
```

# Cause

The text in the messages sent to the LLM triggers one of provider's security measures established to prevent improper use.

# Solution

1. Review the cause of the issue. It is commonly one of JSON keys returned by the error message, in this case "Jailbreak".
2. Relax certain settings if available in the LLM account settings to reduce the level of filtering.

This is the example of Azure OpenAI configuration provided by the provider: [https://learn.microsoft.com/en-us/azure/ai-foundry/openai/how-to/content-filters?view=foundry-classic](https://learn.microsoft.com/en-us/azure/ai-foundry/openai/how-to/content-filters?view=foundry-classic)

The availability of the setting and allowed parameters depend on the LLM provider. This information is intended to instruct the user about potential risks and potential existence of content management settings available, not to prevent or circumvent the provider's content management policy.
