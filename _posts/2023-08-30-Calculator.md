---
toc: true
title: JS Calculator
comments: true
layout: post
description: A common way to become familiar with a language is to build a calculator.  This calculator shows off button with actions.
courses: { compsci: {week: 2} }
type: hacks
---
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        body {
            margin: 0;
            font-family: Arial, sans-serif;
            overflow: hidden;
        }

        .circle-cursor {
            width: 20px;
            height: 20px;
            background-color: #ff5733;
            border-radius: 50%;
            position: absolute;
            transform: translate(-50%, -50%);
            pointer-events: none;
            z-index: 9999;
        }

        .menu-bar {
            background-color: #333;
            color: #fff;
            text-align: center;
            padding: 15px 0;
            position: fixed;
            width: 100%;
            top: 0;
            z-index: 999;
        }

        .menu-bar ul {
            list-style: none;
            padding: 0;
        }

        .menu-bar ul li {
            display: inline;
            margin: 0 20px;
        }

        .menu-bar ul li a {
            color: #fff;
            text-decoration: none;
            transition: all 0.3s ease;
        }

        .menu-bar ul li a:hover {
            color: #ff5733;
        }

        .content {
            padding: 100px;
            text-align: center;
            font-size: 24px;
        }
    </style>
    <title>Fancy Car Website</title>
</head>

<body>
    <div class="circle-cursor"></div>
    <nav class="menu-bar">
        <ul>
            <li><a href="#">Home</a></li>
            <li><a href="#">Cars</a></li>
            <li><a href="#">About</a></li>
            <li><a href="#">Contact</a></li>
        </ul>
    </nav>
    <div class="content">
        <!-- Car images and other content go here -->
        <h1>Welcome to Our Fancy Car Website!</h1>
        <p>Explore our amazing collection of luxury cars.</p>
    </div>
    <script>
        const circleCursor = document.querySelector('.circle-cursor');

        document.addEventListener('mousemove', (e) => {
            const { clientX, clientY } = e;
            circleCursor.style.left = `${clientX}px`;
            circleCursor.style.top = `${clientY}px`;
        });
    </script>
</body>

</html>
