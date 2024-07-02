<script>
  import { onMount } from "svelte";
  import xmlFormatter from "xml-formatter";

  let rawXML = "";
  let formattedXML = "";

  let inputLineNumbers;
  let outputLineNumbers;
  let inputXML;
  let outputXML;

  onMount(() => {
    const savedXML = localStorage.getItem("savedXML");

    if (savedXML) {
      rawXML = savedXML;
      formatXML();
    }
    updateLineNumbers(inputXML, inputLineNumbers);
    updateLineNumbers(outputXML, outputLineNumbers);

    inputXML.addEventListener("input", () =>
      updateLineNumbers(inputXML, inputLineNumbers)
    );
    outputXML.addEventListener("input", () =>
      updateLineNumbers(outputXML, outputLineNumbers)
    );
  });

  function formatXML() {
    try {
      formattedXML = xmlFormatter(rawXML);
    } catch (error) {
      console.error("Error formatting XML:", error);
    }
  }

  function updateLineNumbers(textarea, lineNumbers) {
    if (!textarea || !lineNumbers) return;

    const lines = textarea.value.split("\n").length;
    let numbersHtml = "";
    for (let i = 1; i <= lines; i++) {
      numbersHtml += "<div>" + i + "</div>";
    }
    lineNumbers.innerHTML = numbersHtml;
  }

  function syncScroll(textarea, lineNumbersId) {
    const lineNumbers = document.getElementById(lineNumbersId);
    lineNumbers.scrollTop = textarea.scrollTop;
  }

  function downloadXML() {
    const blob = new Blob([formattedXML], { type: "text/xml" });
    const url = URL.createObjectURL(blob);
    const a = document.createElement("a");
    a.href = url;
    a.download = "formatted.xml";
    document.body.appendChild(a);
    a.click();
    document.body.removeChild(a);
    URL.revokeObjectURL(url);
  }

  function saveXML() {
    localStorage.setItem("savedXML", formattedXML);
    alert("XML has been saved!");
  }

  function clearXML() {
    rawXML = "";
    formattedXML = "";
  }
</script>

<div class="bg-gray-400 h-screen w-full">
  <h1
    class="text-2xl font-bold text-center bg-gradient-to-r from-purple-400 to-red-500 text-transparent bg-clip-text"
  >
    XML Formatter
  </h1>
  <div class="flex items-center justify-center h-full">
    <div
      class="flex flex-col items-start w-full max-w-full p-4 bg-gray-200 rounded-lg shadow-lg"
    >
      <div
        class="flex flex-col md:flex-row w-full space-y-4 md:space-y-0 md:space-x-4"
      >
        <!-- First Textarea Container -->
        <div
          class="flex flex-col items-start w-full md:w-1/2 bg-[#9bc400] rounded-lg p-4 textarea-container"
        >
          <div class="line-numbers" bind:this={inputLineNumbers}></div>
          <label for="inputXML" class="mb-2 text-sm font-medium text-gray-700"
            >Input XML</label
          >
          <textarea
            id="inputXML"
            class="w-full h-64 p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent"
            placeholder="Enter your XML here..."
            bind:this={inputXML}
            on:scroll={() => syncScroll(inputXML, "inputLineNumbers")}
            bind:value={rawXML}
          ></textarea>
        </div>

        <!-- Buttons between the Textareas -->
        <div
          class="flex flex-row md:flex-col justify-center space-x-2 md:space-x-0 md:space-y-2"
        >
          <button
            class="px-4 py-2 text-sm font-medium text-white bg-blue-500 rounded-lg hover:bg-blue-600 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2"
            on:click={formatXML}>Format</button
          >
        </div>

        <!-- Second Textarea Container -->
        <div
          class="flex flex-col items-start w-full md:w-1/2 bg-[#9bc400] rounded-lg p-4 textarea-container"
        >
          <div class="line-numbers" bind:this={outputLineNumbers}></div>
          <label for="outputXML" class="mb-2 text-sm font-medium text-gray-700"
            >Output XML</label
          >
          <textarea
            id="outputXML"
            class="w-full h-64 p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent"
            placeholder="Output will be shown here..."
            bind:this={outputXML}
            on:scroll={() => syncScroll(outputXML, "outputLineNumbers")}
            bind:value={formattedXML}
          ></textarea>
        </div>
      </div>

      <!-- Bottom Buttons -->
      <div
        class="flex flex-col md:flex-row items-center justify-end w-full mt-4 space-y-2 md:space-y-0 md:space-x-2"
      >
        <button
          class="px-4 py-2 text-sm font-medium text-white bg-blue-500 rounded-lg hover:bg-blue-600 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2"
          on:click={downloadXML}>Download</button
        >
        <button
          class="px-4 py-2 text-sm font-medium text-white bg-green-500 rounded-lg hover:bg-green-600 focus:outline-none focus:ring-2 focus:ring-green-500 focus:ring-offset-2"
          on:click={saveXML}>Save</button
        >
        <button
          class="px-4 py-2 text-sm font-medium text-white bg-red-500 rounded-lg hover:bg-red-600 focus:outline-none focus:ring-2 focus:ring-red-500 focus:ring-offset-2"
          on:click={clearXML}>Clear</button
        >
      </div>
    </div>
  </div>
</div>

<style>
  body {
    font-family: "Poppins", sans-serif;
  }
  .textarea-container {
    position: relative;
    display: flex;
    width: 100%;
  }
  .line-numbers {
    position: absolute;
    top: 35px;
    left: 0;
    width: 35px;
    height: calc(100% - 40px);
    border-right: 1px solid #ccc;
    text-align: right;
    padding-right: 5px;
    padding-left: 10px;
    color: #888;
    overflow: hidden;
    font-family: monospace;
    line-height: 1.5em;
  }
  .line-numbers div {
    height: 2em;
  }
  textarea {
    padding-left: 50px;
    font-family: monospace;
    line-height: 1.5em;
    resize: none;
  }
</style>
