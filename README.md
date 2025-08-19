from flask import Flask, request, render_template_string, jsonify

app = Flask(__name__)

tasks = 

HTML_TEMPLATE = """
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Task Manager</title>
</head>
<body>
    <h1>Simple Task Manager</h1>
    <form method="post">
        <input type="text" name="task" placeholder="Enter a new task" required>
        <button type="submit">Add Task</button>
    </form>
    <h2>Tasks:</h2>
    <ul>
        {% for t in tasks %}
            <li>{{ t }}</li>
        {% endfor %}
    </ul>
    <p>API endpoint: <a href="/api/tasks">/api/tasks</a></p>
</body>
</html>
"""

@app.route("/", methods=["GET", "POST"])
def home():
    if request.method == "POST":
        task = request.form.get("task")
        if task:
            tasks.append(task)
    return render_template_string(HTML_TEMPLATE, tasks=tasks)

@app.route("/api/tasks", methods=["GET"])
def get_tasks():
    return jsonify({"tasks": tasks})

if __name__ == "__main__":
    app.run(debug=True)
