<!--
author:   André Dietrich

email:    LiaScript@web.de

version:  0.0.1

edit:     true

language: en

logo:     logo.gif

narrator: UK English Male

comment: This is a chat simulation between different users. Their conversation is defined in a JSON format with support for Markdown and LiaScript elements.

@CHAT: @CHAT_(@uid,```@0```)

@CHAT_
<script run-once modify="false" style="display:block; width:100%; height:460px; border:1px solid #ddd; border-radius:14px; padding:10px; overflow:auto; font-family:sans-serif; font-size:14px; background:#f9f9f9;" id="chat_@0">

const messages = @1

function scrollToBottom() {
    setTimeout(() => {
        const box = document.getElementById("chat_@0");
        if(box)
        box.scrollTo({ top: box.scrollHeight, behavior: "smooth" });
    }, 100)
}

function bubbleHTML(name, text, align, bgColor, nameColor) {
  return `<div style="clear:both; margin:6px 0; text-align:${align};">
<div style="display:inline-block; max-width:70%; background:${bgColor}; border-radius:12px; padding:8px 12px; box-shadow:0 1px 2px rgba(0,0,0,0.15);">
<div style="font-size:11px; font-weight:bold; color:${nameColor}; margin-bottom:3px;">${name}</div>
<div style="font-size:14px; color:#000;">

${
text
}

</div>
</div>
</div>
`
}

function typingHTML(name, align) {
  const bubbleBg = align === "right" ? "#E8F5E9" : "#F1F1F1"
  const nameColor = align === "right" ? "#555" : "#333"
  return `
<div id="typing" style="clear:both; margin:6px 0; text-align:${align};">
<div style="display:inline-block; max-width:70%; background:${bubbleBg}; border-radius:12px; padding:8px 12px; box-shadow:0 1px 2px rgba(0,0,0,0.12);">
<div style="font-size:11px; font-weight:bold; color:${nameColor}; margin-bottom:3px;">${name}</div>
<img src='https://media.tenor.com/eKsWWgnVis0AAAAi/3-points-three-dots.gif' style='height: 10px'>
</div>
</div>
`
}

let confirmed = ""
let typingTimer = null
let dotsStep = 1
let typingCurrent = ""

function showMessage(i) {
  if (i >= messages.length) {
    send.lia("LIA: stop")
    return
  }

  const main = messages[0].name == messages[i].name

  const align = main ? "left" : "right"
  const bgColor = main ? "#FFFFFF" : "#DCF8C6"
  const nameColor = main ? "#333" : "#555"
  const { name, message } = messages[i]

  typingCurrent = typingHTML(name, align)
  send.lia("LIASCRIPT:" + confirmed + typingCurrent)

  setTimeout(() => {
    confirmed += bubbleHTML(name, message, align, bgColor, nameColor)
    send.lia("LIASCRIPT:" + confirmed)
    setTimeout(() => showMessage(i + 1), 2500 * Math.random() + 1000)
  }, 5000 * Math.random())

  scrollToBottom()
}

setTimeout(() => {
  send.lia("")
  showMessage(0)
}, 10)

"LIA: wait"
</script>

@end
-->



# Chat Simulation

    --{{0}}--
Chat Simulation is a LiaScript template designed to create interactive chat-based scenarios for educational or training purposes. It enables authors to simulate conversations between multiple participants, allowing learners to explore different dialogue paths, practice communication skills, or experience branching narratives.

For more information, visit the Chat Simulation GitHub repository.

Try it on LiaScript:

https://liascript.github.io/course/?https://raw.githubusercontent.com/LiaTemplates/Chat-Simulation/main/README.md

See the project on Github:

https://github.com/LiaTemplates/Chat-Simulation

Experiment in the LiveEditor:

https://liascript.github.io/LiveEditor/?/show/file/https://raw.githubusercontent.com/LiaTemplates/Chat-Simulation/main/README.md

    --{{1}}--
Like other LiaScript templates, there are three ways to integrate Chat Simulation, but the easiest way is to copy the import statement into your project. For more information, see the Sec. Implementation.

      {{1}}
1. Load the latest macros via (this might cause breaking changes)

   `import: https://raw.githubusercontent.com/LiaTemplates/Chat-Simulation/main/README.md`

   or the currently latest version `0.0.1`:

   `import: https://raw.githubusercontent.com/LiaTemplates/Chat-Simulation/0.0.1/README.md`

2. Copy the definitions into your Project

3. Clone this repository on GitHub



## `@CHAT`

    --{{0}}--
This is the primary macro to create chat simulations in LiaScript. It allows you to define a conversation between participants, as a list of JSON objects with the parameters `name` and `message`.

```` markdown
``` javascript @CHAT
[
    {name: "Alice", message: "Hello! How are you?"},
    {name: "Bob", message: "I'm good, thanks! How about you?"},
    {name: "Alice", message: "__I'm great!__ Ready to start our project?"},
    {name: "Charlie", message: "Hey everyone!"}
]
```
````

    --{{1}}--
The first participant will always be aligned to the left (main), while all others are aligned to the right. You can use standard Markdown syntax in the `message` field, as well as any LiaScript elements (like charts, multimedia-links, etc.).

      {{1}}
``` javascript @CHAT
[
    {name: "Alice", message: "Hello! How are you?"},
    {name: "Bob", message: "I'm good, thanks! How about you?"},
    {name: "Alice", message: "__I'm great!__ Ready to start our project?"},
    {name: "Charlie", message: "Hey everyone!"}
]
```

## Examples

### Basic Conversation

``` javascript @CHAT
[
  {
    name: 'Mara',
    message:
      'Have you ever heared of LiaScript? It is a Markup language for education?',
  },
  {
    name: 'Oliver',
    message:
      'Ah ... so **LiaScript is basically the same as bitmark** – both are markup languages. 😅',
  },
  {
    name: 'Mara',
    message:
      'Not quite 😉 Sure, both are markup, but their **goals are totally different**.',
  },
  {
    name: 'Mara',
    message:
      '➡️ **bitmark** describes content as small units (*Bits*) that can be standardized and converted into other formats like JSON, H5P, or PDF. See: [bitmark-association.org](https://www.bitmark-association.org/)',
  },
  {
    name: 'Mara',
    message:
      '➡️ **LiaScript** is a Markdown extension that runs **directly in the browser as an interactive course**: with quizzes, text-to-speech, animations, live coding, and macros. See: [liascript.github.io](https://liascript.github.io/)',
  },
  {
    name: 'Oliver',
    message:
      'But wait 🤔 – if both are markup and you can write text + quizzes, isn’t that basically the same thing in the end?',
  },
  {
    name: 'Mara',
    message:
      'Not really. With bitmark you write content that is **transformed** into other formats. With LiaScript you write content that is **immediately runnable online** – with interactive features that bitmark doesn’t have.',
  },
  {
    name: 'Oliver',
    message:
      'Ah, got it now: bitmark = **format & exchange**, LiaScript = **direct executable learning environment**. ✅',
  },
  {
    name: 'Mara',
    message:
      'Exactly **\@Oliver** 👍 LiaScript is more like a **player & language in one**, while bitmark is more of a **data model & conversion tool**.<br><br><img src="https://media0.giphy.com/media/v1.Y2lkPTc5MGI3NjExZGVweW5wbmsyZ3diMWU0eXRzenpyOXJqdWJuMXVxMXNjdTdzMWhhMyZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/axu6dFuca4HKM/giphy.gif">',
  },
]
```

### Interactive LiaScript Elements

``` javascript    @CHAT
[
  {
    name: 'Lena',
    message:
      'Hey 👋 habt ihr schon mit den Mathe-Hausaufgaben angefangen? Thema **quadratische Funktionen**?',
  },
  { name: 'Tom', message: 'Noch nicht 😅 Was war die erste Aufgabe?' },
  {
    name: 'Lena',
    message:
      'Wir sollen die Parabel zu $f(x)=x^2-4x+3$ skizzieren und Scheitel, Nullstellen, Achsensymmetrie angeben.',
  },
  {
    name: 'Maya',
    message:
      'Dann mache ich mal **quadratische Ergänzung**:<br>$x^2-4x+3=(x-2)^2-4+3=(x-2)^2-1$.<br>➡️ **Scheitel**: $S(2\\mid -1)$ 🎯',
  },
  {
    name: 'Ben',
    message:
      'Nullstellen kriegen wir aus $x^2-4x+3=0$.<br>Faktorisieren: $(x-1)(x-3)=0\\Rightarrow x_1=1,\\;x_2=3$ ✅',
  },
  {
    name: 'Tom',
    message:
      'Mit pq-Formel geht’s auch 🧮:<br>$x^2-4x+3=0\\Rightarrow p=-4,\\;q=3$<br>$x=\\frac{-p}{2}\\pm\\sqrt{\\left(\\frac{p}{2}\\right)^2-q}=2\\pm\\sqrt{4-3}=2\\pm1\\Rightarrow 1,3$.',
  },
  {
    name: 'Lena',
    message:
      `<lia-chart style="width: 400px" option="(function () {
  // --- helpers & data ---
  function f(x) { return x*x - 4*x + 3; }

  var XMIN = -2, XMAX = 6, STEP = 0.01;
  var VERTEX = { x: 2, y: f(2) }; // (2, -1)

  function curve() {
    var data = [];
    for (var x = XMIN; x <= XMAX; x += STEP) data.push([x, f(x)]);
    return data;
  }

  // y-range with padding
  var ys = [];
  for (var xi = XMIN; xi <= XMAX; xi += STEP) ys.push(f(xi));
  ys.push(0, VERTEX.y);
  var ymin = Math.min.apply(null, ys), ymax = Math.max.apply(null, ys);
  var pad = Math.max(1, 0.1 * (ymax - ymin || 1));
  var YMIN = Math.floor(ymin - pad), YMAX = Math.ceil(ymax + pad);

  // --- echarts option ---
  var option = {
    grid: { top: 50, left: 55, right: 20, bottom: 50 },
    tooltip: {
      trigger: 'axis',
      formatter: function (params) {
        return params.map(function (p) {
          return p.seriesName + ': (' + p.data[0].toFixed(2) + ', ' + p.data[1].toFixed(2) + ')';
        }).join('<br/>');
      }
    },
    legend: { top: 10, data: ['f(x)', 'Scheitel', 'Nullstellen', 'Achse x=2'] },
    xAxis: {
      name: 'x', min: XMIN, max: XMAX,
      minorTick: { show: true },
      splitLine: { lineStyle: { color: '#999' } },
      minorSplitLine: { show: true, lineStyle: { color: '#ddd' } }
    },
    yAxis: {
      name: 'y', min: YMIN, max: YMAX,
      minorTick: { show: true },
      splitLine: { lineStyle: { color: '#999' } },
      minorSplitLine: { show: true, lineStyle: { color: '#ddd' } }
    },
    series: [
      {
        // Parabel
        name: 'f(x)',
        type: 'line',
        showSymbol: false,
        data: curve()
      },
      {
        // Symmetrieachse x=2
        name: 'Achse x=2',
        type: 'line',
        showSymbol: false,
        lineStyle: { type: 'dashed' },
        data: [[2, YMIN], [2, YMAX]]
      },
      {
        // Scheitelpunkt
        name: 'Scheitel',
        type: 'scatter',
        symbolSize: 10,
        data: [[VERTEX.x, VERTEX.y]]
      },
      {
        // Nullstellen
        name: 'Nullstellen',
        type: 'scatter',
        symbolSize: 9,
        data: [[1, 0], [3, 0]]
      }
    ],
    graphic: [
      { type: 'text', left: 10, top: 30, style: { text: 'Scheitel (2, -1)', fontSize: 12 } },
      { type: 'text', left: 10, top: 48, style: { text: 'Nullstellen: x = 1, 3', fontSize: 12 } },
      { type: 'text', right: 10, top: 30, style: { text: 'Achse: x = 2 (Öffnung ↑)', fontSize: 12, align: 'right' } }
    ]
  };

  return option;
})()
"></lia-chart>`
  },
  {
    name: 'Maya',
    message:
      '**Achsensymmetrie**: Die Parabel ist zu $x=2$ symmetrisch, weil $f(2+h)=f(2-h)$. ✨',
  },
  {
    name: 'Ben',
    message:
      'Was sagt die **Streckung**? Der Faktor vor $x^2$ ist $1$, also Standardweite. Hätte man z. B. $a=2$, wäre sie schmaler.',
  },
  {
    name: 'Tom',
    message:
      'Ich bau schnell die **Scheitelpunktform** nochmal hübsch auf:<br>$f(x)=(x-2)^2-1$. From there: Minimum bei $y=-1$. ✔️',
  },
  {
    name: 'Lena',
    message:
      'Mini-Merker: **Y-Achsenabschnitt** ist $f(0)=3$ ➜ Punkt $(0\\mid3)$.',
  },
  {
    name: 'Maya',
    message:
      "Hab ein kurzes Video dazu gefunden (Scheitelpunkt & pq-Formel) ▶️:<br>!?[](https://www.youtube.com/watch?v=B_PtpvhnNg0)",
  },
  {
    name: 'Ben',
    message:
      "Und noch ein Clip zum **Quadratischen Ergänzen** ▶️:<br>!?[](https://www.youtube.com/watch?v=2zIS89wSh4Q)",
  },
  {
    name: 'Tom',
    message:
      "Wie wäre es mit einem Bild zu **Form-Varianten**?<br> ![Allgemeine Parabel-Formen](https://upload.wikimedia.org/wikipedia/commons/b/b9/Parabeln-var-s.svg)<!-- style='background-color: white; max-width:300px; border:1px solid #ccc;border-radius:8px' -->",
  },
  {
    name: 'Lena',
    message:
      'Nächste Aufgabe: Bestimme die **Parameter** $a,b,c$ aus Punkten. Beispiel: Parabel geht durch $(0\\mid2),(1\\mid0),(3\\mid6)$.<br>Dann lösen wir das LGS aus $f(x)=ax^2+bx+c$. 💡',
  },
  {
    name: 'Maya',
    message:
      'Setzen ein:<br>$c=2$;<br>$a+b+2=0\\Rightarrow a+b=-2$;<br>$9a+3b+2=6\\Rightarrow 9a+3b=4\\Rightarrow 3a+b=\\tfrac{4}{3}$. <br>Subtr.: $(3a+b)-(a+b)=\\tfrac{4}{3}-(-2)\\Rightarrow 2a=\\tfrac{10}{3}\\Rightarrow a=\\tfrac{5}{3}$,<br>$b=-2-a=-2-\\tfrac{5}{3}=-\\tfrac{11}{3}$. ✅',
  },
  {
    name: 'Ben',
    message:
      'Also $f(x)=\\tfrac{5}{3}x^2-\\tfrac{11}{3}x+2$. Scheitel und Nullstellen könnte man jetzt analog bestimmen.',
  },
  {
    name: 'Lena',
    message:
      'Das reicht für heute 😄 Zusammenfassung: $f(x)=x^2-4x+3\\Rightarrow (x-2)^2-1$, **S(2|mid-1)**, Nullstellen **1** & **3**, Achse **x=2**. Danke euch! 🙌',
  }
]
```


## Implementation

    --{{0}}--
The implementation of the chat simulation involves uses two macros, `@CHAT` and `@CHAT_`. Thereby `@CHAT` is used to initiate a chat session with a unique id and passes over the content to `@CHAT_`. `@CHAT_` is then responsible for creating a script that renders the chat interface and handling the message flow.

```` javascript
@CHAT: @CHAT_(@uid,```@0```)

@CHAT_
<script run-once modify="false" style="display:block; width:100%; height:460px; border:1px solid #ddd; border-radius:14px; padding:10px; overflow:auto; font-family:sans-serif; font-size:14px; background:#f9f9f9;" id="chat_@0">

const messages = @1

function scrollToBottom() {
    setTimeout(() => {
        const box = document.getElementById("chat_@0");
        if(box)
        box.scrollTo({ top: box.scrollHeight, behavior: "smooth" });
    }, 100)
}

function bubbleHTML(name, text, align, bgColor, nameColor) {
  return `<div style="clear:both; margin:6px 0; text-align:${align};">
<div style="display:inline-block; max-width:70%; background:${bgColor}; border-radius:12px; padding:8px 12px; box-shadow:0 1px 2px rgba(0,0,0,0.15);">
<div style="font-size:11px; font-weight:bold; color:${nameColor}; margin-bottom:3px;">${name}</div>
<div style="font-size:14px; color:#000;">

${
text
}

</div>
</div>
</div>
`
}

function typingHTML(name, align) {
  const bubbleBg = align === "right" ? "#E8F5E9" : "#F1F1F1"
  const nameColor = align === "right" ? "#555" : "#333"
  return `
<div id="typing" style="clear:both; margin:6px 0; text-align:${align};">
<div style="display:inline-block; max-width:70%; background:${bubbleBg}; border-radius:12px; padding:8px 12px; box-shadow:0 1px 2px rgba(0,0,0,0.12);">
<div style="font-size:11px; font-weight:bold; color:${nameColor}; margin-bottom:3px;">${name}</div>
<img src='https://media.tenor.com/eKsWWgnVis0AAAAi/3-points-three-dots.gif' style='height: 10px'>
</div>
</div>
`
}

let confirmed = ""
let typingTimer = null
let dotsStep = 1
let typingCurrent = ""

function showMessage(i) {
  if (i >= messages.length) {
    send.lia("LIA: stop")
    return
  }

  const main = messages[0].name == messages[i].name

  const align = main ? "left" : "right"
  const bgColor = main ? "#FFFFFF" : "#DCF8C6"
  const nameColor = main ? "#333" : "#555"
  const { name, message } = messages[i]

  typingCurrent = typingHTML(name, align)
  send.lia("LIASCRIPT:" + confirmed + typingCurrent)

  setTimeout(() => {
    confirmed += bubbleHTML(name, message, align, bgColor, nameColor)
    send.lia("LIASCRIPT:" + confirmed)
    setTimeout(() => showMessage(i + 1), 2500 * Math.random() + 1000)
  }, 5000 * Math.random())

  scrollToBottom()
}

setTimeout(() => {
  send.lia("")
  showMessage(0)
}, 10)

"LIA: wait"
</script>

@end
````