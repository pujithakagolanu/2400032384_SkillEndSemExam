# 2400032384_SkillEndSemExam
<!DOCTYPE html>
<html>
<body>

<h2>Student Notes App</h2>

<input id="title" placeholder="Title"><br><br>
<textarea id="content" placeholder="Write note..."></textarea><br><br>
<button onclick="addNote()">Save Note</button>

<ul id="notesList"></ul>

<script>
let notes = JSON.parse(localStorage.getItem("notes")) || [];

function showNotes() {
    document.getElementById("notesList").innerHTML = "";
    notes.forEach((n, i) => {
        document.getElementById("notesList").innerHTML += `
            <li>
                <b>${n.title}</b>: ${n.content}
                <button onclick="editNote(${i})">Edit</button>
                <button onclick="deleteNote(${i})">Delete</button>
            </li>`;
    });
}

function addNote() {
    let title = document.getElementById("title").value;
    let content = document.getElementById("content").value;

    if (editIndex >= 0) {
        notes[editIndex] = { title, content };  
        editIndex = -1;
    } else {
        notes.push({ title, content });
    }

    localStorage.setItem("notes", JSON.stringify(notes));
    showNotes();
    document.getElementById("title").value = "";
    document.getElementById("content").value = "";
}

let editIndex = -1;
function editNote(i) {
    editIndex = i;
    document.getElementById("title").value = notes[i].title;
    document.getElementById("content").value = notes[i].content;
}

function deleteNote(i) {
    notes.splice(i, 1);
    localStorage.setItem("notes", JSON.stringify(notes));
    showNotes();
}

showNotes();
</script>

</body>
</html>
