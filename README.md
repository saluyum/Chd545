
<html lang="de">
<head>
  <meta charset="UTF-8">
  <title>Plotter Designer</title>
  <style>
    body {
      font-family: Arial;
      text-align: center;
      background: #f4f4f4;
      padding: 20px;
    }
    input, select, button {
      padding: 10px;
      margin: 10px;
      font-size: 16px;
    }
    svg {
      border: 1px solid #333;
      margin-top: 20px;
      background: white;
    }
  </style>
</head>
<body>

<h1>Plotter Designer</h1>

<input type="text" id="textInput" placeholder="Text eingeben" value="Hallo">
<br>

<select id="fontSelect">
  <option value="Arial">Arial</option>
  <option value="Courier">Courier</option>
  <option value="Times New Roman">Times</option>
</select>

<br>

<button onclick="generate()">Vorschau</button>
<button onclick="downloadSVG()">SVG Download</button>

<br>

<svg id="canvas" width="500" height="200"></svg>

<script>
function generate() {
  const text = document.getElementById("textInput").value;
  const font = document.getElementById("fontSelect").value;

  const svg = document.getElementById("canvas");
  svg.innerHTML = "";

  const textElement = document.createElementNS("http://www.w3.org/2000/svg", "text");
  textElement.setAttribute("x", 50);
  textElement.setAttribute("y", 100);
  textElement.setAttribute("font-size", 40);
  textElement.setAttribute("font-family", font);
  textElement.textContent = text;

  svg.appendChild(textElement);
}

function downloadSVG() {
  const svg = document.getElementById("canvas").outerHTML;
  const blob = new Blob([svg], {type: "image/svg+xml"});
  const url = URL.createObjectURL(blob);

  const a = document.createElement("a");
  a.href = url;
  a.download = "design.svg";
  a.click();

  URL.revokeObjectURL(url);
}
</script>

</body>
</html>
