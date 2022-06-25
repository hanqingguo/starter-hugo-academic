---
title: Ultrasound Enabled Speaker Authentication

<!-- event: Wowchemy Conference
event_url: https://example.org -->

<!-- location: Hanqing -->
<!-- address:
  street: 450 Serra Mall
  city: Stanford
  region: CA
  postcode: '94305'
  country: United States -->

abstract: "Existing speaker verification techniques distinguish individual speakers via the spectrographic features extracted from an audible frequency range of voice commands. However, they often have high error rates and/or long delays. In this paper, we explore a new direction of human voice research by scrutinizing the unique characteristics of human speech at the ultrasound frequency band. Our research indicates that the high-frequency ultrasound components (e.g. speech fricatives) from 20 to 48 kHz can significantly enhance the security and accuracy of speaker verification. We propose a speaker verification system, which uses a two-stream DNN architecture with a feature fusion mechanism to generate distinctive speaker models. To test the system, we create a speech dataset with 12 hours of audio (9,050 voice samples) from 128 participants. In addition, we create a second spoofed voice dataset to evaluate its security. In order to balance between controlled recordings and real-world applications, the audio recordings are collected from two quiet rooms by 8 different recording devices, including 7 smartphones and an ultrasound microphone. Our evaluation shows that our system achieves 0.58% equal error rate in the speaker verification task, which reduces the best equal error rate of the existing systems by 86.1%. Besides, our system only takes 120 ms for testing an incoming utterance,  within 91 ms processing time, we achieve 0% equal error rate in detecting replay attacks launched by 5 different loudspeakers."

# Talk start and end times.
#   End time can optionally be hidden by prefixing the line with `#`.
date: ""
date_end: ""
all_day: false

# Schedule page publish date (NOT talk date).
publishDate: "2021-5-20T00:00:00Z"

authors: []
tags: []

# Is this a featured talk? (true/false)
featured: false

image:
  caption: 'Image credit: [**shutterstock**](https://www.shutterstock.com/image-vector/voice-authentication-technology-vector-head-profile-1310817581)'
  focal_point: Right

links:
- icon: github
  icon_pack: fab
  name: Demo
  url: https://supervoiceapp.github.io/
url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""

# Markdown Slides (optional).
#   Associate this talk with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides: ""

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects:
- example
---

### **Motivation**:

- **Ultrasound in Speech**: We found that human can produce ultrasound by collecting human speech with a high-end ultrasonic microphone ([CM-16](http://www.avisoft.com/ultrasound-microphones/cm16-cmpa/)). See the experimental setup below:
![setup](testbed.JPG) From the recorded human speech, we analyze the spectrogram and present it to the next figure.
![method](ultrasound_audio.JPG)
It shows that when participants say "*She had your dark suit in greasy wash water all year*", there are some phonemes such as **/sh/**, **/s/**, **/sy/**, **/s/** reach extremely high frequencies (e.g., ~40kHz). The reason why human can produce some ultrasound is the different manners of articulation make different airstream flows. When two speech organs narrow the airstream to cause friction to occur as it passes through, Fricatives are produced. If the airstream is stopped and then released, Stop or Affricate is produced. We found that **fricative**, **stop**, and **affricate** phonemes often carries more energy in ultrasound band.

- **Distinctiveness of Ultrasound**: We extract the speech energies at **fricative**, **stop**, and **affricate** phonemes and summerize them together to represent the identity of the speakers by using $$S_{LTA}(f)=\frac{1}{M}\sum_{t=1}^{N} S(f, p)$$
where `S(f,p)` represents the spectrogram value at frequency `f` and time frame `p`. By comparing the $$S_{LTA}(f)$$ of different participants, we get the following results.
![distinct](distinctive.JPG)
From the left figure, we can see that participants have dispersed speech energies between frequency range from `20kHz-40kHz`, for lower frequencies, we observed similar speech energy trends. The right figure shows the average variance of those speakers, it is evident to show that `16-24kHz`, `24-32kHz` and `32-40kHz` contribute more differences to differentiate participants.

- **Ultrasound Speech for Liveness Detection** Since we find that human can produce some ultrasound, we then use them to detect whether a sound is generated by human or a speaker.
 Through recording the human speech and the replay sound, we present the spectrogram differences as follow: ![liveness](liveness.JPG)
   + Human: Human speech directly recorded by an ultrasound microphone.
   + Scenario1: Attackers record and replay with commercial devices (smart phones).
   + Scenario2: Attackers record with high-end microphones and replay with commercial speakers (smart phones).
   + Scenario3: Attackers record with high-end microphones and replay with ultrasound speakers.

We can observe the apparent difference for four spectrograms. By exploiting this clear differences, we can design our liveness detection algorithm to reach high detection accuracy.

### **Methodology**

![model](model.JPG)
We design a end to end speaker authentication system, which includes a liveness detection module and a speaker verification module. By incorporating the ultrasound component in human speech, we design a <em>**Cumulative energy analysis**</em> method to detect replay attack. Furthermore, we introduce a <em>**two-stream DNN**</em> to handle the low frequency data and the high frequency speech, and fused the extracted feature together to verify the user's voice.

### **Demo**
For more descripitions and **demos** of our collected high frequency human speech, please visit [**Here**](https://supervoiceapp.github.io).
