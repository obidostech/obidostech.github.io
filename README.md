<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>English to Malayalam Translation</title>
<!-- Bootstrap CSS -->
<link href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" rel="stylesheet">
<style>
    .autocomplete-items {
        position: absolute;
        border: 1px solid #d4d4d4;
        border-bottom: none;
        border-top: none;
        z-index: 99;
        top: 100%;
        left: 0;
        right: 0;
    }
    .autocomplete-items div {
        padding: 10px;
        cursor: pointer;
        background-color: #fff; 
        border-bottom: 1px solid #d4d4d4; 
    }
    .autocomplete-items div:hover {
        background-color: #e9e9e9; 
    }
</style>
</head>
<body>
<div class="container">
    <div class="row mt-5">
        <div class="col-12">
            <div class="autocomplete">
                <label for="englishInput">Type English word:</label>
                <input class="form-control" type="text" id="englishInput">
            </div>
            <p>Malayalam Translation: <span id="malayalamOutput"></span></p>
        </div>
    </div>
</div>

<script>
    const translations = {
        "hello": "ഹലോ",
        "where are you": "നീ എവിടെ ആണ്",
        "who are you": "നിങ്ങൾ ആരാണ്"
    };
    const englishWords = Object.keys(translations);

    document.getElementById('englishInput').addEventListener('input', function() {
        let input = this.value;
        closeAllLists();
        if (!input) return false;
        const matchArray = englishWords.filter(word => word.toLowerCase().startsWith(input.toLowerCase()));
        const a = document.createElement("div");
        a.setAttribute("id", this.id + "autocomplete-list");
        a.setAttribute("class", "autocomplete-items");
        this.parentNode.appendChild(a);
        matchArray.forEach(function(item) {
            const b = document.createElement("div");
            b.innerHTML = "<strong>" + item.substr(0, input.length) + "</strong>";
            b.innerHTML += item.substr(input.length);
            b.innerHTML += "<input type='hidden' value='" + item + "'>";
            b.addEventListener("click", function(e) {
                document.getElementById('englishInput').value = this.getElementsByTagName("input")[0].value;
                translateToMalayalam();
                closeAllLists();
            });
            a.appendChild(b);
        });
    });

    function translateToMalayalam() {
        const input = document.getElementById('englishInput').value.toLowerCase();
        const output = document.getElementById('malayalamOutput');
        output.textContent = translations[input] || "Translation not found";
    }

    function closeAllLists(elmnt) {
        var x = document.getElementsByClassName("autocomplete-items");
        for (var i = 0; i < x.length; i++) {
            if (elmnt != x[i] && elmnt != document.getElementById('englishInput')) {
                x[i].parentNode.removeChild(x[i]);
            }
        }
    }

    document.addEventListener("click", function (e) {
        closeAllLists(e.target);
    });
</script>

<!-- Bootstrap JS, Popper.js, and jQuery -->
<script src="https://code.jquery.com/jquery-3.5.1.slim.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.5.2/dist/umd/popper.min.js"></script>
<script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/js/bootstrap.min.js"></script>
</body>
</html>
