<!DOCTYPE html>
<html>
<head>
    <title>Friends Data</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background: #f2f2f2;
            padding: 20px;
        }
        h2 {
            text-align: center;
        }
        input, button {
            width: 100%;
            padding: 8px;
            margin: 6px 0;
        }
        button {
            background: #007BFF;
            color: white;
            border: none;
            cursor: pointer;
        }
        .card {
            background: white;
            padding: 15px;
            margin-top: 15px;
            border-radius: 8px;
        }
        .card h3 {
            margin: 0 0 8px 0;
            color: #333;
        }
    </style>
</head>

<body>

<h2>Friend Information Saver</h2>

<!-- Input Form -->
<input type="text" id="name" placeholder="Friend Name">
<input type="date" id="dob">
<input type="text" id="phone" placeholder="Phone Number">
<input type="text" id="instagram" placeholder="Instagram ID">

<button onclick="saveFriend()">Save</button>

<!-- Output -->
<div id="output"></div>

<script>
function saveFriend() {
    let friend = {
        name: name.value,
        dob: dob.value,
        phone: phone.value,
        instagram: instagram.value
    };

    if (friend.name === "") {
        alert("Name is required");
        return;
    }

    let data = JSON.parse(localStorage.getItem("friends")) || [];
    data.push(friend);
    localStorage.setItem("friends", JSON.stringify(data));

    showFriends();
    clearForm();
}

function showFriends() {
    let data = JSON.parse(localStorage.getItem("friends")) || [];
    output.innerHTML = "";

    data.forEach(f => {
        output.innerHTML += `
            <div class="card">
                <h3>${f.name}</h3>
                <p><b>Date of Birth:</b> ${f.dob || "N/A"}</p>
                <p><b>Phone:</b> ${f.phone || "N/A"}</p>
                <p><b>Instagram:</b> ${f.instagram || "N/A"}</p>
            </div>
        `;
    });
}

function clearForm() {
    name.value = "";
    dob.value = "";
    phone.value = "";
    instagram.value = "";
}

window.onload = showFriends;
</script>

</body>
</html>
