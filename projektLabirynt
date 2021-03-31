var board = [];
var isFind = false;
var length = Infinity;
var dr = [-1, +1, 0, 0];
var dc = [0, 0, +1, -1];
var arrayCheck = [];
var parents = {};
var path = [];
var a;
var b = false;

var button2 = document.getElementById("button2");
button2.addEventListener("click", () => {
    var obstacle = document.getElementById("obstacle");
    board[obstacle.value.split(",")[0]][obstacle.value.split(",")[1]].obstacle = true;
    var sheet = document.createElement("style");
    sheet.classList.add("obstacle");
    var variable = "s" + obstacle.value.split(",")[0] + "_" + obstacle.value.split(",")[1];
    sheet.innerHTML = `.${variable} {background-image: url("Obstacle.png")}`;
    document.body.appendChild(sheet);
});

var button = document.getElementById("button");
button.addEventListener("click", () => {
    var from = document.getElementById("start").value;
    var to = document.getElementById("end").value;
    var tags = document.getElementsByTagName("style");
    for (let i = 0; i < tags.length; i++) {
        if (tags[i].className != "obstacle") {
            tags[i].innerHTML = "";
        }
    }
    parents = {};
    path = [];
    arrayCheck = [];
    queue = [];
    isFind = false;
    a = "";
    for (let i = 0; i < 10; i++) {
        for (let j = 0; j < 10; j++) {
            board[i][j].isVisited = false;
        }
    }
    shortestPath(from.split(",")[0], from.split(",")[1], to.split(",")[0], to.split(",")[1]);
    findingShortestPath(from.split(",")[0], from.split(",")[1]);
    if (b == false) {
        displayingPath("s" + from.split(",")[0] + "_" + from.split(",")[1], "s" + to.split(",")[0] + "_" + to.split(",")[1]);
    } else {
        var variable = "s" + from.split(",")[0] + "_" + from.split(",")[1];
        var sheet = document.createElement("style");
        sheet.innerHTML = `.${variable} {background: #ff652f; background-image: url("End.png")}`;
        document.body.appendChild(sheet);
    }
});

for (let i = 0; i < 100; i++) {
    var newDiv = document.createElement("div");
    newDiv.classList.add("box");
    if (i < 10) {
        newDiv.classList.add("s0_" + i);
    } else {
        newDiv.classList.add("s" + String(i).split("")[0] + "_" + String(i).split("")[1]);
    }
    var visibleBoard = document.getElementsByClassName("visibleBoard");
    visibleBoard[0].appendChild(newDiv);
}

for (let i = 0; i < 10; i++) {
    for (let j = 0; j < 10; j++) {
        board[i] = [];
    }
}

for (let i = 0; i < 10; i++) {
    for (let j = 0; j < 10; j++) {
        board[i][j] = new Object();
        board[i][j].location = `${i},${j}`;
        board[i][j].isVisited = false;
        board[i][j].obstacle = false;
    }
}

function displayingBlueSquares() {
    console.log(arrayCheck);
    while (arrayCheck.length > 0) {
        var variable = "s" + arrayCheck[0].split(",")[0] + "_" + arrayCheck.shift().split(",")[1];
        var sheet = document.createElement("style");
        sheet.innerHTML = `.${variable} {background: blue}`;
        document.body.appendChild(sheet);
    }
}

function displayingPath(start, end) {
    var yes = true;
    var yes2 = true;
    while (path.length > 0) {
        var variable = "s" + path[0].split(",")[0] + "_" + path.shift().split(",")[1];
        var sheet = document.createElement("style");
        if (variable == start) {
            sheet.innerHTML = `.${start} {background: #ff652f; background-image: url("Start.png")}`;
            yes = false;
            document.body.appendChild(sheet);
        } else if (variable == end) {
            sheet.innerHTML = `.${end} {background: #ff652f; background-image: url("End.png")}`;
            yes2 = false;
            document.body.appendChild(sheet);
        } else {
            sheet.innerHTML = `.${variable} {background: #ff652f}`;
            document.body.appendChild(sheet);
        }
    }
}

function shortestPath(r, c, er, ec) {
    if (r + c == er + ec) {
        a = r + "," + c;
        return;
    }
    var rr, cc;
    var queue = [];
    var parent = r + "," + c;
    queue.push(r + "," + c);
    while (queue.length > 0) {
        r = parseInt(queue[0].split(",")[0], 10);
        c = parseInt(queue.shift().split(",")[1], 10);
        parent = r + "," + c;
        for (let i = 0; i < 4; i++) {
            rr = r + dr[i];
            cc = c + dc[i];
            if (rr >= 0 && cc >= 0 && rr < 10 && cc < 10) {
                if (board[rr][cc].isVisited == false) {
                    board[rr][cc].isVisited = true;
                    if (board[rr][cc].obstacle == false) {
                        if (board[rr][cc].location != er + "," + ec) {
                            if (board[rr][cc].location != r + "," + c) {
                                queue.push(rr + "," + cc);
                                arrayCheck.push(rr + "," + cc);
                                parents[rr + "," + cc] = parent;
                            }
                        } else {
                            parents[rr + "," + cc] = parent;
                            isFind = true;
                            console.log("znaleziono wierzchołek");
                            queue = [];
                            break;
                        }
                    } else {
                        var sheet = document.createElement("style");
                        var obstacle = "s" + rr + "_" + cc;
                        sheet.innerHTML = `.${obstacle} {background-image: url("Obstacle.png")}`;
                        document.body.appendChild(sheet);
                    }
                }
            }
        }
        a = er + "," + ec;
    }
    path.push(er + "," + ec);
    if (!isFind) {
        console.log("Nie znaleziono wierzchołka");
    }
}

function findingShortestPath(r, c) {
    do {
        path.push(parents[a]);
        if (a != r + "," + c) {
            a = parents[a];
        } else {
            b = true;
        }
    } while (a != r + "," + c);
}
