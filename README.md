<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
    </head>
    <body onload="getContact()">
        <div id="avatarImage"></div>
        <form id="editForm">
            <label for="firstname">First name</label>
            <input type="text" name="firstname" id="firstname" readonly><br/>
            <label for="lastname">Last name</label>
            <input type="text" name="lastname" id="lastname" readonly><br/>
            <label for="mobile">Mobile</label>
            <input type="text" name="mobile" id="mobile" readonly><br/>
            <label for="email">Email</label>
            <input type="text" name="email" id="email" readonly><br/>
            <label for="avatar" id="avatarLabel" hidden>Change profile image</label><br/>
            <input type="file" name="avatar" id="avatar" hidden><br/>
            <br/>
            <button type="submit" id="submitForm" hidden>Submit</button>
        </form>
        <br/><br/>
        <button id="homeLink" type="button">Home</button>
        <button id="editContact" type="button">Edit</button>
        <button id="deleteContact" type="button">Delete</button>
    
        <script src="config.js"></script>
        <script>
            var id = getId();
            document.getElementById("homeLink").addEventListener('click', homeLink);
            console.log("The id is =" + id); //Corrected!

            function getId(){
                var url = window.location.href;
                var pos = url.search("=");
                var id = url.slice(pos + 1);
                return id;
            }

            fetch(rootPath + "controller/get-contacts/?id=" + id)
            .then(response => {
                console.log("Response status:", response.status);
                 return response.json();
             })
            .then(data => console.log("Fetched Data:", data))
            .catch(error => console.error("Fetch Error:", error));

            function homeLink(){
                window.open("index.html", "_self");
            }

            function displayOuput(data){
                avatarImg = `
                    <img src="${rootPath}/controller/uploads/${data[0].avatat}" width"200"/>
    `
                document.getElementById("avatarImage").innerHTML = avatarImg;
            }
        </script>
    </body>
</html>
