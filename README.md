<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Portfolio + To-Do + Products</title>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body {
      font-family: Arial, sans-serif;
      background: url('https://images.unsplash.com/photo-1522199755839-a2bacb67c546') no-repeat center center fixed;
      background-size: cover;
      color: #333;
    }
    header {
      background:rgb(141, 98, 176);
      color:black;
      padding: 1rem;
      text-align: center;
    }
    nav a {
      margin:  5px;
      color:black;
      text-decoration: none;
      font-weight: bold;
    }
    section {
      padding: 1rem;
      background: black;
      color: white;
      margin: 4rem;
      border-radius: 10px;
    }
    .projects, .contact, .about, .todo, .products {
      margin-bottom: 3rem;
    }
    h2 {
      margin-bottom: 1rem;
    }
    .about-container {
      display: flex;
      flex-wrap: wrap;
      align-items: center;
      gap: 20px;
    }
    .about-container img {
      width: 200px;
      height: 200px;
      border-radius: 50%;
      object-fit: cover;
      border: 3px solid #fff;
    }
    #todoInput { padding: 8px; width: 70%; }
    #addTodo { padding: 8px 16px; margin-left: 10px; cursor: pointer; }
    .todo-item { margin: 8px 0; display: flex; justify-content: space-between; }
    .todo-item button {
      background: red;
      color: white;
      border: none;
      cursor: pointer;
      padding: 4px 8px;
      border-radius: 4px;
    }
    .filters {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
      margin-bottom: 1rem;
    }
    select { padding: 6px; }
    .product-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      gap: 15px;
    }
    .product-card {
      background: black;
      padding: 1rem;
      border: 1px solid #ddd;
      border-radius: 5px;
      color: white;
    }
    .product-card img {
      width: 100%;
      border-radius: 5px;
      margin-bottom: 10px;
    }
    .contact a {
      display: block;
      color: #00ffff;
      text-decoration: underline;
      margin: 10px 0;
      font-size: 1.1em;
    }
    @media (max-width: 600px) {
      nav a {
        display: block;
        margin: 10px 0;
      }
    }
  </style>
</head>
<body>

  <header>
    <h1>My Portfolio</h1>
    <nav>
      <a href="#about">About</a>
      <a href="#projects">Projects</a>
      <a href="#contact">Contact</a>
      <a href="#todo">To-Do</a>
      <a href="#products">Products</a>
    </nav>
  </header>

  <section id="about" class="about">
    <h2>About Me</h2>
    <div class="about-container">
      <img src="raj.jpg" alt="Profile Photo" />
      <p style="flex: 1; min-width: 250px;">
        Hello! I'm a passionate web developer with experience in frontend and backend development. 
        I love building responsive and interactive web apps. This portfolio showcases my skills and projects, 
        including a to-do app and product page with dynamic features.
      </p>
    </div>
  </section>

  <section id="projects" class="projects">
    <h2>Projects</h2>
    <ul>
      <li>Responsive Portfolio Website</li>
      <li>To-Do List with Local Storage</li>
      <li>Product Filter and Sort Page</li>
    </ul>
  </section>

  <section id="contact" class="contact">
    <h2>Contact</h2>
    <a href="srajuvarla@gmail.com">📧 srajuvarla@gmail.com</a>
    <a href="https://www.linkedin.com/in/your-linkedin" target="_blank">🔗 LinkedIn Profile</a>
    <a href="https://github.com/Raj-1718hub" target="_blank">💻 https://github.com/Raj-1718hub</a>
  </section>

  <section id="todo" class="todo">
    <h2>To-Do / Notes</h2>
    <input type="text" id="todoInput" placeholder="Enter task or note..." />
    <button id="addTodo">Add</button>
    <div id="todoList"></div>
  </section>

  <section id="products" class="products">
    <h2>Product Page</h2>
    <div class="filters">
      <select id="categoryFilter">
        <option value="">All Categories</option>
        <option value="Tech">Tech</option>
        <option value="Clothing">Clothing</option>
      </select>
      <select id="priceFilter">
        <option value="">All Prices</option>
        <option value="low">Under $50</option>
        <option value="high">Over $50</option>
      </select>
      <select id="sortBy">
        <option value="">Sort By</option>
        <option value="rating">Rating (High to Low)</option>
      </select>
    </div>
    <div id="productGrid" class="product-grid"></div>
  </section>

  <script>
    // To-Do List with Local Storage
    const todoInput = document.getElementById('todoInput');
    const addTodo = document.getElementById('addTodo');
    const todoList = document.getElementById('todoList');

    function renderTodos() {
      const todos = JSON.parse(localStorage.getItem('todos')) || [];
      todoList.innerHTML = '';
      todos.forEach((todo, i) => {
        const div = document.createElement('div');
        div.className = 'todo-item';
        div.innerHTML = `<span>${todo}</span> <button onclick="deleteTodo(${i})">Delete</button>`;
        todoList.appendChild(div);
      });
    }

    function deleteTodo(index) {
      const todos = JSON.parse(localStorage.getItem('todos')) || [];
      todos.splice(index, 1);
      localStorage.setItem('todos', JSON.stringify(todos));
      renderTodos();
    }

    addTodo.onclick = () => {
      const task = todoInput.value.trim();
      if (!task) return;
      const todos = JSON.parse(localStorage.getItem('todos')) || [];
      todos.push(task);
      localStorage.setItem('todos', JSON.stringify(todos));
      todoInput.value = '';
      renderTodos();
    };

    window.onload = renderTodos;

    // Product Filter and Sort with Images
    const products = [
      {
        name: 'Laptop',
        category: 'Tech',
        price: 999,
        rating: 4.8,
        image: "pc.jpg"
      },
      {
        name: 'T-Shirt',
        category: 'Clothing',
        price: 25,
        rating: 4.2,
        image: "ts.jpg"  
      },
      {
        name: 'Smartphone',
        category: 'Tech',
        price: 699,
        rating: 4.6,
        image: "px.jpg"
      },
      {
        name: 'Jeans',
        category: 'Clothing',
        price: 60,
        rating: 4.1,
        image: "jeans.jpg"
      }
    ];

    const productGrid = document.getElementById('productGrid');
    const categoryFilter = document.getElementById('categoryFilter');
    const priceFilter = document.getElementById('priceFilter');
    const sortBy = document.getElementById('sortBy');

    function renderProducts() {
      let filtered = [...products];

      if (categoryFilter.value) {
        filtered = filtered.filter(p => p.category === categoryFilter.value);
      }

      if (priceFilter.value === 'low') {
        filtered = filtered.filter(p => p.price < 50);
      } else if (priceFilter.value === 'high') {
        filtered = filtered.filter(p => p.price >= 50);
      }

      if (sortBy.value === 'rating') {
        filtered.sort((a, b) => b.rating - a.rating);
      }

      productGrid.innerHTML = '';
      filtered.forEach(p => {
        const card = document.createElement('div');
        card.className = 'product-card';
        card.innerHTML = `
          <img src="${p.image}" alt="${p.name}" />
          <h3>${p.name}</h3>
          <p>Category: ${p.category}</p>
          <p>Price: $${p.price}</p>
          <p>Rating: ${p.rating}</p>
        `;
        productGrid.appendChild(card);
      });
    }

    categoryFilter.onchange = priceFilter.onchange = sortBy.onchange = renderProducts;
    renderProducts();
  </script>
</body>
</html> 
