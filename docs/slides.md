---
theme: signalwerk
title: "OpenAI API and <br>**Open Source Alternatives**"
---

```fm
style: negative
background: true
```

## Hello _LiipConf 2023 👋_

# {{process.content.frontmatter.title}}

_Which One is Right for You?_

<footer>

2023 · Zurich · Stefan Huber

</footer>

--s--

```fm
style: image
background:
  image: https://portrait.signalwerk.ch/illustration/2020/rgb/w4000/stefan-huber.jpg
  position: 50% 40%
```

## Stefan

<div class="box box--w40p box--bottom box--white box--padding small">

- Joined Liip 2019 · <small>2<sup>nd</sup> AFK LiipConf</small>
- Developer · Drupal ZH
- ❦ Typography · <small>`U+2766 FLORAL HEART`</small>

</div>

<footer class="footer--right">

Illustration by [Benjamin Güdel](http://www.guedel.biz/) · 2020

</footer>

--s--

## Objective of the session

- **OpenAI API** & (open) _alternatives_
- **LLM** · basics
- _ideas_ and **concepts**
- Integration into _client projects_

<br>

> I try to give you inputs, not solutions

--s--

## Non-Objective of the session

### This session is not about <br>_ethics_ and **legal** impact

> OpenAI/ChatGPT is not a <br>[Highly-Trusted Service](https://docs.google.com/document/d/1jlm6Cj-dHXbEcT8PSFHYPTxmP00S4Fj43ZMKJKtVSuk/edit#heading=h.fsuhhrmrgwbi) for Liip!

--s--

## Disclaimer

- I am **not** an _AI/ML expert_
- We are all having different _backgrounds/knowhow_

<br>

> Let's make it great with a Q & A at the end and share your thoughts/projects

--s--

## LiipConf 2023

- **2:15 PM – 3:00 PM** <br>[... && ZueriCityGPT – the search for the city of zurich, which doesn't suck](https://2023.conf.liip.ch/event/liipconf-2023-1/track/vendure-io-the-open-source-headless-e-commerce-which-doesn-t-suck-zuericitygpt-the-search-for-the-city-of-zurich-which-doesn-t-suck-30) <br>Christian Stocker
- **3:10 PM – 3:55 PM** <br>[Unlocking AI's Potential: The Next Steps for Liip](https://2023.conf.liip.ch/event/liipconf-2023-1/track/unlocking-ais-potential-the-next-steps-for-liip-35) <br>Jonathan Fiagbedzi, Stefan Huber, Max Reichen, Fabio Santschi

--s--

```fm
style: negative
background: true
```

## Let's do it _programmatically_

# OpenAI **API**

--s--

## Who is OpenAI?

- _2015_: `OpenAI, Inc.` is a **non-profit** research company
- _2019_: `OpenAI, L.P.` is a **for-profit** company
- profit capped to **100 times of investment**

--s--

## Security/Privacy

- What _data_ do you send to the provider?
- OpenAI _learns on ChatGPT_ (opt-out)
- OpenAI _does not learn on API-Requests_

<footer>

Source: [OpenAI · Terms of use · 3. Content · (c) Use of Content to Improve Services](https://openai.com/policies/terms-of-use) (Version: March 14, 2023)

</footer>

--s--

## Microsoft Azure

- [Same API](https://azure.microsoft.com/en-us/products/cognitive-services/openai-service/) as OpenAI
- _Models from OpenAI_ hosted by Microsoft
- Almost the [same pricing](https://azure.microsoft.com/en-us/pricing/details/cognitive-services/openai-service/) as OpenAI
- Offers [**EU hosting**](https://azure.microsoft.com/en-us/explore/global-infrastructure/products-by-region/?products=cognitive-services&regions=switzerland-north,switzerland-west,europe-north,europe-west) (Netherlands)
- Many [ISO-Certificates](https://learn.microsoft.com/en-us/azure/compliance/offerings/offering-iso-27001)

--s--

## OpenAI API Keys and Management

- API-Access needs an _API-Key_ → contact `#ai-exchange`
- The [API-Key](https://platform.openai.com/account/api-keys) is bound to _your OpenAI User_
- _Name_ your API-Keys
- Be aware of your _organization's_

--s--

## Tokens

- Tokens are the _smallest unit_ of input
- Tokens are _not words_ but a set of **vocabulary**
- Each model has a _different tokens_ and _size limits_

<br>

### Example

`GPT-3.5-turbo` can process _4096 tokens_. If you have more than 4096 tokens, you need to split your request into multiple requests.

<footer>

Test: [OpenAI · Tokenizer](https://platform.openai.com/tokenizer)

</footer>

--s--

## Pricing

- You _pay_ for Text _per Token_ (see [pricing](https://openai.com/pricing))
- Usually **super cheap** (Liip in Q1 & Q2 2023 ~ $ 15)

<footer>

<small>In theory you can have a request that costs (~ $ 1)</small>

</footer>

--s--

## Models

- **GPT-3.5-turbo** <br>fast & not so smart <small>(it's cheap for API use)</small>
- **GPT-3.5-turbo-16k** <br>many tokens for context & fast & not so smart <br><small>(it's cheap for API use)</small>
- **GPT-4** <br>slow & smarter <small>(it's expensive for API use)</small>

<footer>

Reference: [OpenAI · Models](https://platform.openai.com/docs/models)

</footer>

--s--

## Rule of thumb

> _GPT-3.5_ is good enough for _common tasks_  
> Use _GPT-4_ for more _complex tasks_ (like writing code)

--s--

## APIs offered by OpenAI

- `/completions` - Text Completion
- `/chat/completions` - Text conversation (chat)
- `/embeddings` - Get embeddings for text
- `/edits` - Work on existing text
- `/images/generations` – Create images from text
- `/audio/transcriptions` – Transcribe audio to text

> Test in [_playground_](https://platform.openai.com/playground) (no GPT-4 in Liip Account)

<footer>

Reference: [OpenAI · API Reference](https://platform.openai.com/docs/api-reference)

</footer>

--s--

## API-Requests

You send a request to a specific model.

<div style="font-size: 0.8em">

```js
fetch("https://api.openai.com/v1/...", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    Authorization: `Bearer ${OPENAI_API_KEY}`,
    "OpenAI-Organization": `${OPENAI_API_ORG}`,
  },
  body: JSON.stringify({
    /* data */
  }),
});
```

</div>

--s--

## `/completions`

### Example

<mark class="mark--prompt">A hello world in Perl is:</mark><mark><br>#!/usr/bin/perl<br>print "Hello World\n";</mark>

- **pro**: Very simple to parse answer
- **con**: Sometimes hard to request

--s--

## `/chat/completions`

<div style="font-size: 0.55em">

```js
[
  {
    role: "system",
    content: `You are ChatGPT, a large language model trained by OpenAI.
    Answer as concisely as possible. Knowledge cutoff: 2021-09-01.
    Current date: 2023-06-29`,
  },
  {
    role: "user",
    content: "Write me a hello world in Perl.",
  },
  {
    role: "assistant",
    content: "Certainly! Here's a hello world program in Perl: …",
  },
];
```

</div>

- **pro**: Simple to request
- **con**: Parsing is sometimes harder

--s--

## Completion · _instructions_

<mark class="mark--prompt">Write a hello world in JavaScript</mark>

<mark>Welcome to my first article in this series on JavaScript. I'm going to show you how to create a hello world application in JavaScript.</mark>

<footer>

Model: `text-ada-001` (June 2023)

</footer>
--s--

## Completion · _instructions_

<mark class="mark--prompt">Q: Write a hello world in JavaScript.<br>A:</mark><mark> console.log('Hello World!');</mark>

<footer>

Model: `text-davinci-003` (June 2023)

</footer>

--s--

## Zero-shot learning

<mark class="mark--prompt">Translate English to German:<br>chees →</mark><mark> Käse</mark>

<footer>

Model: `text-davinci-003` (June 2023)

</footer>

--s--

## Zero-shot learning

<mark class="mark--prompt">Translate English to German:<br>chees →</mark><mark><br>permissions →</mark>

<footer>

Model: `text-ada-001` (June 2023)

</footer>

--s--

## One-shot learning

<mark class="mark--prompt">Translate English to German:<br>table → Tisch<br>chees →</mark><mark> Käse</mark>

<footer>

Model: `text-davinci-003` & `text-ada-001` (June 2023)

</footer>

--s--

## Few-shot learning

<mark class="mark--prompt">Translate English to German:<br>table → Tisch<br>to run → laufen<br>capitalism → Kapitalismus<br>chees →</mark><mark> Käse</mark>

<footer>

Model: `text-davinci-003` & `text-ada-001` (June 2023)

</footer>

--s--

## `/embeddings`

- Generate a _vector for a text_
- Compare vectors to _find similar texts_
- _Contextual_ understanding
- [Blog-Post soon up](https://www.liip.ch/en/blog/ai-multilingual-search?token=06a407d5294d552ae5578b277f799f44bce839a0)

--s--

```fm
style: negative
background: true
```

## There's more …

# _Open Source_ <br>alternatives for LLMs

--s--

## OpenAI vs. Open Models

- _OpenAI_ has currently _advanced models_ for text generation
- _Open Source alternatives_ for large language models
- Currently we have _LLama-Derivated_ Models as strong Open Source alternatives
- _LLama_ was computed by _Meta_ but is not open/libre

--s--

## Comparison

<div class="grid" style="font-size:0.7em">
<div class="col6">

## GPT-3 (2020)

- 50 257 vocabulary size
- 2048 context length
- 175 B parameters
- Trained on 300 B tokens
- _GPU cost ~ 1 – 10 mio USD_

</div>
<div class="col6">

## LLaMA (2023)

- 32 000 vocabulary size
- 2048 context length
- 65 B parameters
- Trained on 1 – 1.4 T tokens
- _GPU cost ~ 5 mio USD_

</div>
</div>

<footer>

Source: [Microsoft Build 2023 · State of GPT](https://www.youtube.com/watch?v=bZQun8Y4L2A)

<footer>

--s--

## What's available?

- _Foundation_ Models
- **Fine-tuned** Models (often instruction models)

--s--

## Foundation Models

- Training on a _large corpus of text_
- _General purpose_ language models
- _Can be fine-tuned_ for specific tasks
- _Predict the next word_ (completion not instruction)

--s--

## Foundation Models

- Not _task_ specific
- Not _domain_ specific
- Not _data_ specific
- Not _language_ specific (ideally)

--s--

## Instruction Models

- Optimized for _«chat-like»_ interactions
- Feels _like ChatGPT_

--s--

## LLaMA ecosystem

### Based on LLaMA

- [Alpaca](https://crfm.stanford.edu/2023/03/13/alpaca.html)
- [Vicuna](https://lmsys.org/blog/2023-03-30-vicuna/)
- [Koala](https://bair.berkeley.edu/blog/2023/04/03/koala/)
- …

--s--

## In the spirit of LLaMA

- [RedPajama](https://www.together.xyz/blog/redpajama-7b)
- [GPT4All](https://gpt4all.io/index.html)
- [StarCoder](https://huggingface.co/blog/starcoder)
- [OpenLLaMA](https://github.com/openlm-research/open_llama)
- …

--s--

# The problems

- On _«normal» hardware_ you can rund <br>max. ~ 13 B models
- The Models are most of the time in _english_
- _Slowish_
- _80 %_ of a GPT-4 is a _huge difference_
- $ 10k+ GPU can run the bigger models
- You can run it in datacenters ($ ~30/h)

--s--

## Falcon · the new star

- Available at [HuggingFace](https://huggingface.github.io/text-generation-inference/)
- _Multi-lingual_
- Completely _Open Source_ & libre
- Smaller sizes can be handled by a normal GPU
- [Test](https://huggingface.co/tiiuae/falcon-7b-instruct?text=Give+me+3+things+to+do+in+Paris.)

--s--

```fm
style: negative
background: true
```

## Run it locally

# Try _it!_

--s--

## Fast Chat

- Simple instructions [FastChat](https://github.com/lm-sys/FastChat)
- Test different LLMs quickly
- Offers _OpenAI compatible API_

--s--

## Example for Search bs.ch

- [Proof of Concept](https://basel.search.srv.signalwerk.ch/) with OpenAI
- Test A: Embeddings with [Sentence-BERT Multi-Lingual Model](https://www.sbert.net/docs/pretrained_models.html#multi-lingual-models)
- Test B:
  1. Translate to English with [No Language Left Behind](https://ai.facebook.com/research/no-language-left-behind/)
  2. Embeddings with LLaMA

--s--

```fm
style: negative
background: true
```

## Interleave generation _🥳_

# What you can do _with LLaMA_ but **not with OpenAI**

--s--

## Guidance

<div style="font-size: 0.7em">

The following is a character profile for an RPG game in JSON format.

```json
{
    "id": "{{id}}",
    "description": "{{description}}",
    "name": "{{gen 'name'}}",
    "age": {{gen 'age' pattern='[0-9]+' stop=','}},
    "armor": "{{#select 'armor'}}leather{{or}}chainmail{{or}}plate{{/select}}",
    "weapon": "{{select 'weapon' options=valid_weapons}}",
    "class": "{{gen 'class'}}",
    "mantra": "{{gen 'mantra' temperature=0.7}}",
    "strength": {{gen 'strength' pattern='[0-9]+' stop=','}},
    "items": [{{#geneach 'items' num_iterations=5 join=', '}}"{{gen 'this' temperature=0.7}}"{{/geneach}}]
}
```

</div>

<footer>

Source: [Microsoft Guidance](https://github.com/microsoft/guidance)

</footer>

--s--

## Guidance

![](./img/json_animation.gif)

<footer>

Source: [Microsoft Guidance](https://github.com/microsoft/guidance)

</footer>

--s--

```fm
style: negative
background: true
```

## LLM is not the end

# _Open Source_ alternatives for other stuff

--s--

## Overview

- [Stable Diffusion](https://stability.ai/blog/stable-diffusion-public-release) – for image generation
- [Whisper](https://github.com/openai/whisper) – for speech recognition
- [No Language Left Behind](https://ai.facebook.com/research/no-language-left-behind/) – translations
- …

--s--

```fm
style: negative
background: true
```

## exit 0; thx

# Questions?
