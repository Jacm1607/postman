{
  "guestId": "{{guestId}}",
  "hostId": "{{hostId}}",
  "name": "{{name}}"
}




------------------------------------
pre script

let chats = JSON.parse(pm.environment.get("chats"));
console.log()
let iActual = parseInt(pm.environment.get("indice"));

if(iActual >= chats.length){
    iActual = 0;
}

let item = chats[iActual];

pm.environment.set("name", item.name);
pm.environment.set("guestId", item.guestId);
pm.environment.set("hostId", item.hostId);


----------------------------------

let iActual = parseInt(pm.environment.get("indice"));
let chats = JSON.parse(pm.environment.get("chats"));

let chat = chats[iActual];

// TEST 1°
pm.test(`Status code: ${chat.status}`, function () {
    pm.response.to.have.status(chat.status);
});

if (chat.status == 201) {
    // Test status code 201
    pm.test("La respuesta devuelve un GUID", function () {
        const response = pm.response.text();
        console.log(response)
        const guidRegex = /^\"[0-9A-Fa-f]{8}-[0-9A-Fa-f]{4}-[0-9A-Fa-f]{4}-[0-9A-Fa-f]{4}-[0-9A-Fa-f]{12}\"$/;
        pm.expect(response).to.match(guidRegex);
    });
}

if (chat.status == 400) {
    // Test status code 400
}


iActual = iActual + 1;
if (iActual >= chats.length) {
    iActual = 0;
}
pm.environment.set("indice", iActual);




