## [Helsinki-NLP/opus-mt-en-fr](https://huggingface.co/Helsinki-NLP/opus-mt-en-fr)

```4d
var $OpenAI : cs.AIKit.OpenAI

var $customHeaders : Object
$customHeaders:={}

var $ChatCompletionsParameters : Object
$ChatCompletionsParameters:={}
$ChatCompletionsParameters.input:="The cat sat on the mat"

/*
	
	over-ride AI Kit behaviour
	
*/

$ChatCompletionsParameters.body:=Formula from string("$0:={messages: Null; input: This.input}")

$OpenAI:=cs.AIKit.OpenAI.new({customHeaders: $customHeaders})
$OpenAI.baseURL:="http://127.0.0.1:8080/v1"
var $ChatCompletionsResult : cs.AIKit.OpenAIChatCompletionsResult
$ChatCompletionsResult:=$OpenAI.chat.completions.create(Null; $ChatCompletionsParameters)

var $translations : Collection
$translations:=$ChatCompletionsResult.request.response.body.translations

If ($translations#Null)
	var $text : Text
	$text:=$translations.at(0).text.at(0)
	ALERT($text)
End if 
```

<img width="480" height="159" alt="Screenshot 2026-03-18 at 22 46 51" src="https://github.com/user-attachments/assets/60b2b22b-5311-4d5a-b3ea-8e37430045d5" />

https://miyako.github.io/CTranslate2/translate
