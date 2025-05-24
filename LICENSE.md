<!DOCTYPE html><html lang="bn">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>বাংলা লেখা থেকে ভয়েস</title>
  <style>
    body { font-family: Kalpurush, sans-serif; padding: 20px; background: #f0f0f0; }
    textarea { width: 100%; height: 150px; font-size: 18px; padding: 10px; }
    button { margin: 10px 5px; padding: 10px 15px; font-size: 16px; }
  </style>
</head>
<body>
  <h2>বাংলা লেখাকে কণ্ঠে রূপ দিন</h2>
  <textarea id="text" placeholder="এখানে বাংলায় লিখুন..."></textarea><br>
  <button onclick="speak('male')">পুরুষ কণ্ঠ</button>
  <button onclick="speak('female')">নারী কণ্ঠ</button>
  <button onclick="speak('child')">শিশু কণ্ঠ</button>  <script>
    function speak(voiceType) {
      const text = document.getElementById('text').value;
      const utterance = new SpeechSynthesisUtterance(text);
      utterance.lang = 'bn-BD';

      const voices = window.speechSynthesis.getVoices();
      let selectedVoice = voices.find(v => v.lang === 'bn-BD');

      if (voiceType === 'female') {
        selectedVoice = voices.find(v => v.name.toLowerCase().includes('female')) || selectedVoice;
      } else if (voiceType === 'male') {
        selectedVoice = voices.find(v => v.name.toLowerCase().includes('male')) || selectedVoice;
      } else if (voiceType === 'child') {
        selectedVoice = voices.find(v => v.name.toLowerCase().includes('child')) || selectedVoice;
      }

      if (selectedVoice) utterance.voice = selectedVoice;
      speechSynthesis.speak(utterance);
    }

    // Load voices for speech synthesis
    window.speechSynthesis.onvoiceschanged = () => {
      window.speechSynthesis.getVoices();
    };
  </script></body>
</html>
