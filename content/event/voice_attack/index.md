---
title: Black-Box, Query-Efficient Audio Adversarial Attacks

<!-- event: Wowchemy Conference
event_url: https://example.org -->

<!-- location: Hanqing -->
<!-- address:
  street: 450 Serra Mall
  city: Stanford
  region: CA
  postcode: '94305'
  country: United States -->

abstract: "Our audio adversarial attacks is a query efficient black-box attack towards voice assistants. Existing black-box adversarial attacks on voice assistants either apply substitution models or leverage the intermediate model output to estimate the gradients for crafting adversarial audio samples. However, these attack approaches require a significant amount of queries with a lengthy training stage. Our attack leverages the decision-based attack to produce effective adversarial audios, and reduces the number of queries by optimizing the gradient estimation. In the experiments, we perform our attack against 4 different speech-to-text APIs under 3 real-world scenarios to demonstrate the real-time attack impact. The results also show that our attack is practical and robust in attacking 5 popular commercial voice controllable devices over the air. The benchmark result shows we can generate adversarial examples and launch the attack in a couple of minutes. We improve the query efficiency and reduce the cost of a successful untargeted and targeted adversarial attack by 93.1% and 65.5% compared with the state-of-the-art black-box attacks, using only∼300 and∼1,500 queries, respectively."

# Talk start and end times.
#   End time can optionally be hidden by prefixing the line with `#`.
date: ""
date_end: ""
all_day: false

# Schedule page publish date (NOT talk date).
publishDate: "2021-01-01T00:00:00Z"

authors: []
tags: []

# Is this a featured talk? (true/false)
featured: false

<!-- image:
  caption: 'Image credit: [**Unsplash**](https://unsplash.com/photos/bzdhc5b3Bxs)'
  focal_point: Left -->

links:
- icon: twitter
  icon_pack: fab
  name: Follow
  url: https://twitter.com/guohahaha1
url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""

# Markdown Slides (optional).
#   Associate this talk with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides: example

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects:
- example
---

### **Motivation**:

- **Query-Inefficient**: Existing black box audio attacks require plenty of queries to interact with the victim speech models, e.g., [Devil's whisper](https://www.usenix.org/system/files/sec20summer_chen-yuxuan_prepub.pdf) attacks commercial speech to text model by training an substitute model through querying victim model. [OCCAM](https://arxiv.org/pdf/2110.09714.pdf) estimates the gradient by incorporating evolutionary algorithms. The extensive query is time consuming, costly and may attract attention.

- **Decision-Boundary**: We find that the decision boundary in speech to text model is different from it in computer vision models. Due to the non-contiguous decision boundary, it's hard for attacker to initialize the perturbation.

- **Phoneme** We find a short phoneme can surprisingly alter the speech model prediction. Based on the observation, we decide to optimize the duration and power of phoneme to inject it attacking the speech to text model.

### **Methodology**
![method](method.JPG) There are three stages to generate a perturbation. At stage 1, given an input audio, we inject many different phonemes to it and try to alter the transcript result. Next, we collect the phonemes or phoneme combinations to a perturbation set. At stage 3, we estimate the gradient by applying small changes to the candidate perturbation, and then estimate the gradient direction through observing the prediction result changes. Then apply the estimated gradient to fine tuning the perturbation. Finally, we can get the adversarial perturbation targeting to a input audio.

<!-- ### **Demo**
<div>
<table>
<tr>
	<td>Bob and Alice talk simultaneously</td>
	<td>Only Alice's voice is kept</td>
</tr>
<tr>
	<td><audio controls>
		  <source src="./assets/joint.wav" type="audio/wav">
		  Your browser does not support the <code>audio</code> element.
		</audio></td>
	<td><audio controls>
		  <source src="./assets/joint-focus.wav" type="audio/wav">
		  Your browser does not support the <code>audio</code> element.
		</audio></td>
</tr>
</table>
</div> -->
