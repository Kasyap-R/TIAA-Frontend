<script>
    export let text = '';
  </script>
  
  <style>
    .question-container {
      font-family: 'Arial', sans-serif; /* This can be changed to any modern font you prefer */
      font-size: 1.8rem; /* Adjust size as needed */
      color: #333; /* A modern and readable color */
      padding: 20px;
      margin-bottom: 30px; /* Space before the answer options start */
      text-align: center; /* Centers the text in the container */
      border-bottom: 2px solid #eee; /* A subtle line to separate the question from answers */
      max-width: 800px; /* Max width to maintain readability */
      margin: 0 auto 30px; /* Centering the container */
    }
  </style>
  
  <div class="question-container">
    {text}
  </div>
  