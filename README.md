# Aiii
<!DOCTYPE html>
<html lang="bn">
<head>
    <meta charset="UTF-8">
    <title>Mubin AI Assistant</title>
    <style>
        body { background: #0f172a; color: white; display: flex; justify-content: center; padding-top: 50px; font-family: sans-serif; }
        .container { width: 450px; background: #1e293b; padding: 25px; border-radius: 15px; box-shadow: 0 4px 15px rgba(0,0,0,0.5); }
        input { width: 95%; padding: 12px; margin-bottom: 15px; border-radius: 8px; border: none; }
        button { width: 100%; padding: 12px; background: #38bdf8; border: none; border-radius: 8px; color: white; cursor: pointer; font-weight: bold; }
        #response { margin-top: 20px; white-space: pre-wrap; color: #cbd5e1; }
    </style>
</head>
<body>

<div class="container">
    <h3>Mubin AI</h3>
    <input type="text" id="userInput" placeholder="আপনার নির্দেশ লিখুন...">
    <button onclick="getAIResponse()">Send</button>
    <div id="response"></div>
</div>

<script>
    async function getAIResponse() {
        // আপনার API Key এখানে বসান
        const apiKey = "AIzaSyAdvFQh5K9k1rBm1XzbyX3IashrR59pZgA"; 
        const prompt = document.getElementById('userInput').value;
        const responseDiv = document.getElementById('response');
        
        responseDiv.innerText = "অপেক্ষা করুন...";

        try {
            const response = await fetch('https://api.openai.com/v1/chat/completions', {
                method: 'POST',
                headers: {
                    'Authorization': `Bearer ${apiKey}`,
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify({
                    model: "gpt-4o",
                    messages: [
                        {
                            role: "system", 
                            // আপনার ইনস্ট্রাকশনগুলো এখানে লিখুন:
                            content: "তুমি মুবিনের পার্সোনাল এআই। তুমি অত্যন্ত বাধ্য এবং শুধুমাত্র আমার নির্দেশ অনুযায়ী কাজ করো। তুমি কোনো হ্যাকিং বা ক্ষতিকর কাজে সাহায্য করবে না, বরং প্রফেশনাল এবং সঠিক সমাধান দেবে।" 
                        }, 
                        {
                            role: "user", 
                            content: prompt
                        }
                    ]
                })
            });
            
            const data = await response.json();
            responseDiv.innerText = data.choices[0].message.content;
        } catch (error) {
            responseDiv.innerText = "এরর হয়েছে! আপনার API Key ঠিক আছে কি না যাচাই করুন।";
        }
    }
</script>
</body>
</html>
