let deviceID = "DEV-" + Math.random().toString(36).substring(2,10).toUpperCase();

document.getElementById("deviceID").innerText = deviceID;

// STORAGE (simulate database)
let requests = [];
let licenseDB = {};

// SEND TO ADMIN
function sendToAdmin(){
    requests.push(deviceID);
    document.getElementById("status").innerText = "Sent to Admin ✔";

    renderRequests();
}

// SHOW REQUESTS IN ADMIN PANEL
function renderRequests(){
    let box = document.getElementById("requests");
    box.innerHTML = "";

    requests.forEach((id,index)=>{
        box.innerHTML += `
            <div style="padding:5px;background:#0f172a;margin:5px;">
                ${id}
                <button onclick="selectDevice('${id}')">Select</button>
            </div>
        `;
    });
}

let selectedDevice = "";

// SELECT DEVICE FOR LICENSE
function selectDevice(id){
    selectedDevice = id;
    alert("Selected: " + id);
}

// GENERATE LICENSE KEY
function generateKey(){
    if(!selectedDevice){
        alert("Select device first");
        return;
    }

    let key = "ZMI-" + Math.random().toString(36).substring(2,10).toUpperCase();

    licenseDB[selectedDevice] = key;

    document.getElementById("genKey").value = key;

    alert("License generated for " + selectedDevice);
}

// ACTIVATE USER SIDE
function activate(){
    let key = document.getElementById("licenseKey").value;

    if(licenseDB[deviceID] === key){
        alert("✅ Activated Successfully");
    } else {
        alert("❌ Invalid Key");
    }
}
