<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8">
		<meta name="viewport" content="width=device-width, initial-scale=1.0">
		<title>XML Formatter</title>
		<link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
		<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;700&display=swap" rel="stylesheet">
		<style>
		  body {
			font-family: 'Poppins', sans-serif;
		  }
		</style>
	  </head>
	  
	  
<body class="bg-gray-400 h-screen w-full">
	<h1 class="text-2xl font-bold text-center bg-gradient-to-r from-purple-400 to-red-500 text-transparent bg-clip-text">
		XML Formatter
	  </h1>
	  

<div class="flex items-center justify-center h-full">
  <div class="flex flex-col items-start w-full max-w-full p-4 bg-gray-200 rounded-lg shadow-lg">
    <div class="flex flex-col md:flex-row w-full space-y-4 md:space-y-0 md:space-x-4">
      <!-- First Textarea Container -->
      <div class="flex flex-col items-start w-full md:w-1/2 bg-[#9bc400] rounded-lg p-4">
        <label for="inputXML" class="mb-2 text-sm font-medium text-gray-700">Input XML</label>
        <textarea id="inputXML" class="w-full h-64 p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent" placeholder="Enter your XML here..."></textarea>
      </div>

      <!-- Buttons between the Textareas -->
      <div class="flex flex-row md:flex-col justify-center space-x-2 md:space-x-0 md:space-y-2">
        <button class="px-4 py-2 text-sm font-medium text-white bg-blue-500 rounded-lg hover:bg-blue-600 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2" onclick="transformXML();">Format</button>
      </div>

      <!-- Second Textarea Container -->
      <div class="flex flex-col items-start w-full md:w-1/2 bg-[#9bc400] rounded-lg p-4">
        <label for="outputXML" class="mb-2 text-sm font-medium text-gray-700">Output XML</label>
        <textarea id="outputXML" class="w-full h-64 p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent" placeholder="Output will be shown here..."></textarea>
      </div>
    </div>

    <!-- Bottom Buttons -->
    <div class="flex flex-col md:flex-row items-center justify-end w-full mt-4 space-y-2 md:space-y-0 md:space-x-2">
      <button class="px-4 py-2 text-sm font-medium text-white bg-blue-500 rounded-lg hover:bg-blue-600 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2" onclick="downloadXML();">Download</button>
      <button class="px-4 py-2 text-sm font-medium text-white bg-green-500 rounded-lg hover:bg-green-600 focus:outline-none focus:ring-2 focus:ring-green-500 focus:ring-offset-2" onclick="saveXML();">Save</button>
      <button class="px-4 py-2 text-sm font-medium text-white bg-red-500 rounded-lg hover:bg-red-600 focus:outline-none focus:ring-2 focus:ring-red-500 focus:ring-offset-2" onclick="clearXML();">Clear</button>
    </div>
  </div>
</div>

</body>
</html>