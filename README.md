# Anki Minimal Language Learning Template

A custom language learning template designed for Anki

## Preview

![https://github.com/leonluleonlu/anki-minimal-language-learning-template/blob/master/media/Comprehension.png](https://github.com/leonluleonlu/anki-minimal-language-learning-template/blob/master/media/Comprehension.png)

## Design principles

Ever since I started using Anki to memorise things many years ago, I have always come to the realisation that certain design principles will make my flashcards effective. Yet when I looked online recently to find out if someone has made templates that follows such principle, I found none, and so I decided to make one.

1. **Visual definition first.** Human brains (at least my brain, if there's any dispute) process images much faster than words. With visual information over translation, foreign words build associations with the actual object instead of a word in a language you already know, this bypasses the processes of having to think of a word and then its translation.
2. **Less is more.** When reviewing, fields such as example sentences and definitions are collapsed by default to reduce visual cluttering, while translations are hidden as a second-level hint. By doing so, you can focus on trying to recollect what you want to remember instead of getting distracted. To see the hidden fields, simply hover the mouse cursor over its title.
3. **Flexible card types.** Two fields included in the template ("add reverse" and "add spell") controls how Anki generates additional cards from new notes. A reverse card simply asks you for the word given the image or the definition, whereas a spelling card asks you to type the word.
4. **Speech synthesis.** Instead of spending time looking for the right recording, the template uses Anki's built-in {{tts}} field to generate audio.
5. **It has to look nice :)**

### Comprehension Cards

![https://github.com/leonluleonlu/anki-minimal-language-learning-template/blob/master/media/Comprehension%20.gif](https://github.com/leonluleonlu/anki-minimal-language-learning-template/blob/master/media/Comprehension%20.gif)

### Reverse (or recollection) Cards

![https://github.com/leonluleonlu/anki-minimal-language-learning-template/blob/master/media/Recollection.gif](https://github.com/leonluleonlu/anki-minimal-language-learning-template/blob/master/media/Recollection.gif)

### Spelling Cards

![https://github.com/leonluleonlu/anki-minimal-language-learning-template/blob/master/media/Spelling.gif](https://github.com/leonluleonlu/anki-minimal-language-learning-template/blob/master/media/Spelling.gif)

## How to get the template

The easy way is to simply download and import the [apkg](https://github.com/leonluleonlu/anki-minimal-language-learning-template/releases/download/1.0/Minimal.Language.Learning.Demo.Deck.v1.apkg) file into Anki.

Do note that this template only contains English and French voice synthesis and is created and only tested on MacOS. To match your target language and operating system, configure the `{{tts}}` fields in the card template accordingly. Please refer to [the Anki manual](https://docs.ankiweb.net/#/templates/fields?id=text-to-speech) for more information.

The hard way is to create the card yourself with the following code.

### Card 1 (Comprehension) Front

```html
<p style="text-align: right; font-size: 12px; margin-bottom: -20px; color: #bbb">comprehension</p>

<span class="serif bold bigbigbig primary">{{stem}}</span>
	
<span class="sans " style="margin-left: 7px">{{part of speech}}</span><br>
	
<span class="sans big light-primary italic">{{word}}</span>
<span class="sans" style="margin-left: 7px">{{IPA}}</span>{{tts fr_FR voices=Apple_Thomas speed=1.2:stem}}<br>
	
<div class="section-title bold small verylightcolour" onmouseover="showExample()">EXAMPLE(S)</div>

<div  id="example" style="display: none">
	<div class="sans text"  >{{example(s)}}</div>
	<div class="light-primary italic text add-top-margin small sans">{{hint:translation of example(s)}}</div>
</div>

<script>
  function showDefinition() {
    document.getElementById("definition").style.display = "block";
  }
  function showExample() {
    document.getElementById("example").style.display = "block";
  }
</script>
```

### Card 1 (Comprehension) Back

```html
{{FrontSide}}

<script>
  showExample()
</script>

{{#image}}
<div class="section-title bold small verylightcolour" id=answer>IMAGE</div>
	{{image}}
{{/image}}

<div  class="">
	<div class="section-title bold small verylightcolour" onmouseover="showDefinition()">DEFINITION</div>

	<div class="sans" id="definition" style="display: none">

		<div class="lightcolour text">{{definition}}</div>

		<div class="italic text light-primary small add-top-margin">{{hint:word translation}}</div>

	</div>
</div>

<div class="section-title bold small verylightcolour">EXTRA NOTES</div>
	<div class="normal text">{{edit:notes}}</div>
```

### Card 2 (Reverse) Front

```html
{{#add reverse? (type anything to add recollection card)}}

<p style="text-align: right; font-size: 12px; margin-bottom: -20px; color: #bbb">recollection</p>

<!--if image-->
{{#image}}
	<div style="height: 10px"></div>
	{{image}}
{{/image}}

<div  class="">

	{{#image}}
		<div class="section-title bold small verylightcolour" onmouseover="showDefinition()">DEFINITION/TRANSLATION</div>
	{{/image}}

<!--if image-->
{{#image}}
	<div class="sans" id="definition" style="display: none">
{{/image}}

<!--if no image-->
{{^image}}
	<div class="sans" id="definition" style="display: block">
{{/image}}

		<div class="lightcolour text">{{definition}}</div>

		<div class="italic text light-primary small add-top-margin">{{hint:word translation}}</div>

	</div>
</div>

<div class="section-title bold small verylightcolour" onmouseover="showNotes()">EXTRA NOTES</div>
<div class="sans" id="notes" style="display: none">	
	<div class="normal text">{{edit:notes}}</div>

</div>

<script>
  function showDefinition() {
    document.getElementById("definition").style.display = "block";
  }
  function showExample() {
    document.getElementById("example").style.display = "block";
  }
  function showNotes() {
    document.getElementById("notes").style.display = "block";
  }
</script>

{{/add reverse? (type anything to add recollection card)}}
```

### Card 2 (Reverse) Back

```html
{{FrontSide}}

<div class="section-title bold small verylightcolour" id=answer style="margin-bottom: 4px">WORD</div>
<span class="serif bold bigbigbig primary">{{stem}}</span>
	
<span class="sans " style="margin-left: 7px">{{part of speech}}</span><br>
	
<span class="sans big light-primary italic">{{word}}</span>
<span class="sans" style="margin-left: 7px">{{IPA}}</span>{{tts  fr_FR voices=Apple_Thomas speed=1.2:stem}}<br>
	
<div class="section-title bold small verylightcolour" onmouseover="showExample()">EXAMPLE(S)</div>

<div  id="example" style="display: none">
	<div class="sans text"  >{{example(s)}}</div>
	<div class="light-primary italic text add-top-margin small sans">{{hint:translation of example(s)}}</div>
</div>

<script>
  //showExample()
</script>
```

### Card 3 (Spelling) Front

```html
{{#add spell? (type anything to add spelling card)}}

<p style="text-align: right; font-size: 12px; margin-bottom: -20px; color: #bbb">spelling</p>

<!--if image-->
{{#image}}
	<div style="height: 10px"></div>
	{{image}}
{{/image}}

<div  class="">

	{{#image}}
		<div class="section-title bold small verylightcolour" onmouseover="showDefinition()">DEFINITION/TRANSLATION</div>
	{{/image}}

<!--if image-->
{{#image}}
	<div class="sans" id="definition" style="display: none">
{{/image}}

<!--if no image-->
{{^image}}
	<div class="sans" id="definition" style="display: block">
{{/image}}

		<div class="lightcolour text">{{definition}}</div>

		<div class="italic text light-primary small add-top-margin">{{hint:word translation}}</div>

	</div>

<div class="section-title bold small verylightcolour" onmouseover="showDefinition()">PRONUNCIATION</div>
<span class="sans" style="margin-left: 7px">{{IPA}}</span>{{tts  fr_FR voices=Apple_Thomas speed=1.2:stem}}<br>

<div class="section-title bold small verylightcolour" id=answer >SPELL</div>
<span class="serif bold bigbigbig black">{{type:stem}}</span>

<script>
  function showDefinition() {
    document.getElementById("definition").style.display = "block";
  }
  function showExample() {
    document.getElementById("example").style.display = "block";
  }
  function showNotes() {
    document.getElementById("notes").style.display = "block";
  }
</script>

{{/add spell? (type anything to add spelling card)}}
```

### Card 3 (Spelling) Back

```html
{{FrontSide}}

<br>

<script>
  //showExample()
</script>
```

### Style

```css
/* Layout */

.card {
	font-family: "Gill Sans", Helvetica, Arial;
	font-size: 1.4rem;
	text-align: center;
	color: #4B515D;
	background-color: white;
	height: 100%;
	max-width: 760px;
	margin-left: auto;
	margin-right: auto;
	align-self: center;
}

hr.hr-block {
	border: 2px solid #7eb1fc; width:200px; margin-top: 20px; margin-bottom: 20px;
	max-width: 200px
}

.section-title {
	display: flex;
	align-items: center;
	text-align: center;
	font-family: "Futrura", "Gill Sans", Helvetica, Arial;
	letter-spacing: 0.3rem;
	margin-top: 12px;
	margin-bottom: 12px;
/*	max-width: 500px; */
	margin-left: auto;
	margin-right: auto;
}

.section-title::before,
.section-title::after {
	content: "";
	flex: 1;
	border-bottom: 1px solid #dfe8ec;
}

.section-title::before {
	margin-right: 1em;
}

.section-title::after {
	margin-left: 0.7em;
}

img {
	min-width: 350px;
	max-width 500px;
}

/* Play button */

.replay-button {
    margin: 0px;
}
.replay-button svg {
	width: 16px;
	height: 16px;
}
.replay-button svg circle {
	fill: white;
}
.replay-button svg path {
	stroke: white;
	fill: #0d47a1;
}

/* Typography */

.serif {
	font-family: "Georgia", Times New Romen;
}
.sans {
	font-family: "Futura", "Gill Sans", Helvetica, Arial;
}
.bold {
	font-weight: bold;
}
.light {
	font-weight: light;
}
.italic {
	font-style: italic;
}
.title {
	color: #4285F4;
	font-size: 0.8rem;
}
b {
	color: #0d47a1;
}
u {
}
i {
}
.bigbigbig {
	font-size: 1.9rem
}
.bigbig {
	font-size: 1.4rem
}
.big {
	font-size: 1.2rem
}
.normal {
	font-size 1rem
}
.small {
	font-size: 0.96rem
}
.smallsmall {
	font-size: 0.7rem
}
.smallsmallsmall {
	font-size: 0.5rem
}
.primary, a {
	color: #0d47a1
}
.light-primary {
	color: #4285F4
}
.lightcolour {
	color: #3E4551
}
.verylightcolour {
	color: #90a4ae
}

.text {
	max-width:700px;
	margin-left: auto;
	margin-right: auto;
	align-self: center;
}

.add-top-margin {
	margin-top: 5px
}

.black {
	color: black
}

/* type */

.typeGood {
	background: #8af28a;
}
.typeBad {
	background: #fca897
}
.typeMissed {
	background: #d5d5d5
}

input {
	font-family: "Georgia", Times New Romen !important;
}

input:focus, textarea:focus, select:focus{
	outline: none;
	text-align: center;
	font-weight: bold;
	color: #0d47a1;
}

#typeans {
	font-size: 1.9rem;
	margin-top: 10px;
}
```
