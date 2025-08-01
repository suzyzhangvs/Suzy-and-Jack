# Suzy-and-Jack
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>老板的点餐系统</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Microsoft YaHei', Arial, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
            background: white;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #ff6b6b, #ee5a24);
            color: white;
            text-align: center;
            padding: 30px;
        }

        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }

        .header p {
            font-size: 1.2em;
            opacity: 0.9;
        }

        .main-content {
            display: flex;
            min-height: 600px;
        }

        .menu-section {
            flex: 2.5;
            padding: 30px;
            background: #f8f9fa;
        }

        .category-tabs {
            display: flex;
            margin-bottom: 30px;
            background: white;
            border-radius: 10px;
            overflow: hidden;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }

        .category-tab {
            flex: 1;
            padding: 15px 20px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s ease;
            border: none;
            background: white;
            font-size: 1.1em;
            font-weight: bold;
            color: #7f8c8d;
        }

        .category-tab.active {
            background: linear-gradient(135deg, #3498db, #2980b9);
            color: white;
        }

        .category-tab:hover:not(.active) {
            background: #ecf0f1;
        }

        .category-content {
            display: none;
        }

        .category-content.active {
            display: block;
        }

        .category-title {
            font-size: 1.8em;
            color: #2c3e50;
            margin-bottom: 20px;
            text-align: center;
            padding: 15px;
            background: linear-gradient(135deg, #74b9ff, #0984e3);
            color: white;
            border-radius: 10px;
            text-shadow: 1px 1px 2px rgba(0,0,0,0.3);
        }

        .menu-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
        }

        .menu-item {
            background: white;
            border-radius: 15px;
            padding: 0;
            box-shadow: 0 5px 20px rgba(0,0,0,0.1);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            border-left: 5px solid #3498db;
            overflow: hidden;
        }

        .menu-item:hover {
            transform: translateY(-8px);
            box-shadow: 0 12px 30px rgba(0,0,0,0.15);
        }

        .menu-item-image {
            width: 100%;
            height: 200px;
            object-fit: cover;
            border-radius: 15px 15px 0 0;
            transition: transform 0.3s ease;
            background: linear-gradient(45deg, #f1f2f6, #ddd);
        }

        .menu-item:hover .menu-item-image {
            transform: scale(1.05);
        }

        .menu-item-image[src*="data:image/svg"] {
            background: linear-gradient(135deg, #667eea, #764ba2);
        }

        .menu-item-content {
            padding: 25px;
        }

        .menu-item h3 {
            color: #2c3e50;
            font-size: 1.4em;
            margin-bottom: 12px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .menu-item .price {
            color: #e74c3c;
            font-size: 1.6em;
            font-weight: bold;
            margin-bottom: 15px;
        }

        .menu-item .description {
            color: #7f8c8d;
            font-size: 0.95em;
            margin-bottom: 20px;
            line-height: 1.5;
        }

        .quantity-control {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 15px;
            margin-bottom: 20px;
        }

        .quantity-control button {
            width: 40px;
            height: 40px;
            border: none;
            border-radius: 50%;
            background: #3498db;
            color: white;
            font-size: 1.3em;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .quantity-control button:hover {
            background: #2980b9;
            transform: scale(1.1);
        }

        .quantity-control button:disabled {
            background: #bdc3c7;
            cursor: not-allowed;
            transform: none;
        }

        .quantity-input {
            width: 70px;
            text-align: center;
            border: 2px solid #ecf0f1;
            border-radius: 8px;
            padding: 10px;
            font-size: 1.1em;
            font-weight: bold;
        }

        .add-to-cart {
            width: 100%;
            padding: 15px;
            background: linear-gradient(135deg, #2ecc71, #27ae60);
            color: white;
            border: none;
            border-radius: 10px;
            font-size: 1.1em;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .add-to-cart:hover {
            background: linear-gradient(135deg, #27ae60, #229954);
            transform: translateY(-3px);
        }

        .cart-section {
            flex: 1;
            background: #2c3e50;
            color: white;
            padding: 30px;
        }

        .cart-header {
            text-align: center;
            margin-bottom: 30px;
        }

        .cart-header h2 {
            font-size: 1.8em;
            margin-bottom: 10px;
        }

        .cart-item {
            background: #34495e;
            padding: 15px;
            margin-bottom: 12px;
            border-radius: 10px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            transition: all 0.3s ease;
        }

        .cart-item:hover {
            background: #3b4c63;
        }

        .cart-item-info {
            flex: 1;
        }

        .cart-item-name {
            font-weight: bold;
            margin-bottom: 5px;
            font-size: 1.1em;
        }

        .cart-item-details {
            font-size: 0.9em;
            opacity: 0.8;
        }

        .cart-item-price {
            font-weight: bold;
            color: #f39c12;
            font-size: 1.1em;
        }

        .remove-btn {
            background: #e74c3c;
            border: none;
            color: white;
            padding: 8px 12px;
            border-radius: 6px;
            margin-left: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .remove-btn:hover {
            background: #c0392b;
            transform: scale(1.05);
        }

        .order-time-section {
            background: #34495e;
            padding: 20px;
            border-radius: 10px;
            margin: 20px 0;
        }

        .order-time-title {
            color: white;
            font-size: 1.2em;
            margin-bottom: 15px;
            text-align: center;
            font-weight: bold;
        }

        .time-options {
            display: flex;
            gap: 10px;
            margin-bottom: 15px;
        }

        .time-option {
            flex: 1;
            padding: 10px;
            background: #2c3e50;
            color: white;
            border: 2px solid #34495e;
            border-radius: 8px;
            cursor: pointer;
            text-align: center;
            transition: all 0.3s ease;
            font-size: 0.9em;
        }

        .time-option.active {
            background: #3498db;
            border-color: #2980b9;
        }

        .time-option:hover {
            background: #3498db;
        }

        .datetime-inputs {
            display: none;
            gap: 10px;
            margin-top: 10px;
        }

        .datetime-inputs.show {
            display: flex;
        }

        .datetime-input {
            flex: 1;
            padding: 10px;
            border: 2px solid #34495e;
            border-radius: 6px;
            background: white;
            font-size: 0.9em;
        }

        .datetime-input:focus {
            border-color: #3498db;
            outline: none;
        }

        .selected-time {
            background: #2c3e50;
            padding: 10px;
            border-radius: 6px;
            text-align: center;
            margin-top: 10px;
            color: #f39c12;
            font-size: 0.9em;
        }

        .cart-total {
            background: #e74c3c;
            padding: 25px;
            border-radius: 12px;
            text-align: center;
            margin: 25px 0;
        }

        .cart-total h3 {
            font-size: 1.5em;
            margin-bottom: 15px;
        }

        .total-amount {
            font-size: 2.2em;
            font-weight: bold;
        }

        .submit-order {
            width: 100%;
            padding: 18px;
            background: linear-gradient(135deg, #f39c12, #e67e22);
            color: white;
            border: none;
            border-radius: 12px;
            font-size: 1.3em;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .submit-order:hover {
            background: linear-gradient(135deg, #e67e22, #d35400);
            transform: translateY(-3px);
        }

        .submit-order:disabled {
            background: #7f8c8d;
            cursor: not-allowed;
            transform: none;
        }

        .clear-cart {
            width: 100%;
            padding: 12px;
            background: transparent;
            color: #e74c3c;
            border: 2px solid #e74c3c;
            border-radius: 10px;
            font-size: 1em;
            cursor: pointer;
            margin-top: 15px;
            transition: all 0.3s ease;
        }

        .clear-cart:hover {
            background: #e74c3c;
            color: white;
        }

        .empty-cart {
            text-align: center;
            opacity: 0.7;
            padding: 50px 20px;
        }

        .category-icon {
            font-size: 1.2em;
        }

        @media (max-width: 768px) {
            .main-content {
                flex-direction: column;
            }
            
            .menu-grid {
                grid-template-columns: 1fr;
            }
            
            .header h1 {
                font-size: 2em;
            }

            .category-tabs {
                flex-direction: column;
            }

            .time-options {
                flex-direction: column;
                gap: 8px;
            }

            .datetime-inputs {
                flex-direction: column;
                gap: 8px;
            }

            .order-time-title {
                font-size: 1.1em;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🍽️ 老板的点餐系统</h1>
            <p>欢迎来到美食天堂，享受最优质的餐饮体验 - 精选分类菜品</p>
        </div>

        <div class="main-content">
            <div class="menu-section">
                <div class="category-tabs">
                    <button class="category-tab active" onclick="showCategory('staple')">
                        <span class="category-icon">🍚</span> 主食
                    </button>
                    <button class="category-tab" onclick="showCategory('soup')">
                        <span class="category-icon">🍲</span> 汤品
                    </button>
                    <button class="category-tab" onclick="showCategory('stirfry')">
                        <span class="category-icon">🥘</span> 炒菜
                    </button>
                    <button class="category-tab" onclick="showCategory('specialty')">
                        <span class="category-icon">⭐</span> 特色菜
                    </button>
                </div>

                <!-- 主食类 -->
                <div id="staple" class="category-content active">
                    <div class="category-title">🍚 主食类</div>
                    <div class="menu-grid" id="stapleGrid">
                        <!-- 主食菜品将通过JavaScript生成 -->
                    </div>
                </div>

                <!-- 汤品类 -->
                <div id="soup" class="category-content">
                    <div class="category-title">🍲 汤品类</div>
                    <div class="menu-grid" id="soupGrid">
                        <!-- 汤品将通过JavaScript生成 -->
                    </div>
                </div>

                <!-- 炒菜类 -->
                <div id="stirfry" class="category-content">
                    <div class="category-title">🥘 炒菜类</div>
                    <div class="menu-grid" id="stirfryGrid">
                        <!-- 炒菜将通过JavaScript生成 -->
                    </div>
                </div>

                <!-- 特色菜类 -->
                <div id="specialty" class="category-content">
                    <div class="category-title">⭐ 特色菜类</div>
                    <div class="menu-grid" id="specialtyGrid">
                        <!-- 特色菜将通过JavaScript生成 -->
                    </div>
                </div>
            </div>

            <div class="cart-section">
                <div class="cart-header">
                    <h2>🛒 购物车</h2>
                    <p>已选择 <span id="cartCount">0</span> 件商品</p>
                </div>

                <div id="cartItems">
                    <div class="empty-cart">
                        <p>购物车还是空的</p>
                        <p>快去选择您喜欢的菜品吧！</p>
                    </div>
                </div>

                <div class="order-time-section">
                    <div class="order-time-title">📅 订单时间</div>
                    <div class="time-options">
                        <div class="time-option active" onclick="selectTimeOption('now')">
                            🚀 立即下单
                        </div>
                        <div class="time-option" onclick="selectTimeOption('scheduled')">
                            ⏰ 预约时间
                        </div>
                    </div>
                    <div class="datetime-inputs" id="datetimeInputs">
                        <input type="date" class="datetime-input" id="orderDate" onchange="updateSelectedTime()">
                        <input type="time" class="datetime-input" id="orderTime" onchange="updateSelectedTime()">
                    </div>
                    <div class="selected-time" id="selectedTime">
                        选择的时间：立即下单
                    </div>
                </div>

                <div class="cart-total">
                    <h3>总计</h3>
                    <div class="total-amount">¥<span id="totalAmount">0.00</span></div>
                </div>

                <button class="submit-order" id="submitOrder" disabled onclick="submitOrder()">
                    提交订单
                </button>
                <button class="clear-cart" onclick="clearCart()">
                    清空购物车
                </button>
            </div>
        </div>
    </div>

    <script>
        // 按分类组织的菜品数据
        const menuData = {
            staple: [
                {id: 1, name: "蚂蚁上树", price: 25.00, description: "粉丝爽滑，肉末香浓，口感丰富", icon: "🍜", image: "https://images.unsplash.com/photo-1569718212165-3a8278d5f624?w=400&h=300&fit=crop&crop=faces"},
                {id: 2, name: "扬州炒饭", price: 22.00, description: "粒粒分明，配菜丰富，经典主食", icon: "🍚", image: "https://images.unsplash.com/photo-1603133872878-684f208fb84b?w=400&h=300&fit=crop&crop=faces"},
                {id: 3, name: "红烧排骨面", price: 28.00, description: "面条劲道，排骨香浓，汤汁浓郁", icon: "🍝", image: "https://images.unsplash.com/photo-1555126634-323283e090fa?w=400&h=300&fit=crop&crop=faces"},
                {id: 4, name: "牛肉拉面", price: 26.00, description: "手工拉面，牛肉鲜嫩，汤头醇厚", icon: "🍜", image: "https://images.unsplash.com/photo-1569718212165-3a8278d5f624?w=400&h=300&fit=crop&crop=center"},
                {id: 5, name: "韭菜猪肉蒸饺", price: 20.00, description: "皮薄馅大，韭菜香浓，手工制作", icon: "🥟", image: "https://images.unsplash.com/photo-1496116218417-1a781b1c416c?w=400&h=300&fit=crop&crop=center"}
            ],
            soup: [
                {id: 6, name: "蒸蛋羹", price: 15.00, description: "嫩滑如丝，营养丰富，老少皆宜", icon: "🥚", image: "https://images.unsplash.com/photo-1588566565463-180a5b2090d2?w=400&h=300&fit=crop&crop=center"},
                {id: 7, name: "紫菜蛋花汤", price: 12.00, description: "清淡鲜美，营养丰富，家常汤品", icon: "🍲", image: "https://images.unsplash.com/photo-1547592180-85f173990554?w=400&h=300&fit=crop&crop=center"},
                {id: 8, name: "冬瓜排骨汤", price: 32.00, description: "清香解腻，排骨酥烂，汤汁清甜", icon: "🍲", image: "https://images.unsplash.com/photo-1547592166-23ac45744acd?w=400&h=300&fit=crop&crop=center"},
                {id: 9, name: "酸辣汤", price: 18.00, description: "酸辣开胃，口感丰富，经典川菜", icon: "🌶️", image: "https://images.unsplash.com/photo-1547592180-85f173990554?w=400&h=300&fit=crop&crop=faces"},
                {id: 10, name: "银耳莲子汤", price: 16.00, description: "滋阴润燥，甜润可口，养生佳品", icon: "🍯", image: "https://images.unsplash.com/photo-1547592166-23ac45744acd?w=400&h=300&fit=crop&crop=faces"}
            ],
            stirfry: [
                {id: 11, name: "宫保鸡丁", price: 28.00, description: "经典川菜，鸡丁嫩滑，花生酥脆", icon: "🐔", image: "https://images.unsplash.com/photo-1512058564366-18510be2db19?w=400&h=300&fit=crop&crop=center"},
                {id: 12, name: "麻婆豆腐", price: 22.00, description: "四川名菜，麻辣鲜香，豆腐嫩滑", icon: "🌶️", image: "https://images.unsplash.com/photo-1606491956689-2ea866880c84?w=400&h=300&fit=crop&crop=center"},
                {id: 13, name: "鱼香肉丝", price: 26.00, description: "川菜经典，甜酸微辣，回味无穷", icon: "🐟", image: "https://images.unsplash.com/photo-1512058564366-18510be2db19?w=400&h=300&fit=crop&crop=faces"},
                {id: 14, name: "青椒肉丝", price: 24.00, description: "家常小炒，清香爽脆，营养均衡", icon: "🫑", image: "https://images.unsplash.com/photo-1565299624946-b28f40a0ca4b?w=400&h=300&fit=crop&crop=center"},
                {id: 15, name: "西红柿鸡蛋", price: 18.00, description: "经典搭配，酸甜开胃，营养丰富", icon: "🍅", image: "https://images.unsplash.com/photo-1565299624946-b28f40a0ca4b?w=400&h=300&fit=crop&crop=faces"}
            ],
            specialty: [
                {id: 16, name: "红烧肉", price: 35.00, description: "传统家常菜，肥瘦相间，入口即化", icon: "🥩", image: "https://images.unsplash.com/photo-1544025162-d76694265947?w=400&h=300&fit=crop&crop=center"},
                {id: 17, name: "水煮鱼", price: 45.00, description: "麻辣鲜香，鱼肉嫩滑，汤汁浓郁", icon: "🐟", image: "https://images.unsplash.com/photo-1565299507177-b0ac66763828?w=400&h=300&fit=crop&crop=center"},
                {id: 18, name: "清蒸鲈鱼", price: 48.00, description: "鱼肉鲜美，营养丰富，制作精细", icon: "🐠", image: "https://images.unsplash.com/photo-1544943910-4c1dc44aab44?w=400&h=300&fit=crop&crop=center"},
                {id: 19, name: "白切鸡", price: 38.00, description: "粤菜名品，鸡肉鲜嫩，原汁原味", icon: "🐔", image: "https://images.unsplash.com/photo-1598103442097-8b74394b95c6?w=400&h=300&fit=crop&crop=center"},
                {id: 20, name: "口水鸡", price: 33.00, description: "川菜凉菜，麻辣鲜香，口感丰富", icon: "🌶️", image: "https://images.unsplash.com/photo-1598103442097-8b74394b95c6?w=400&h=300&fit=crop&crop=faces"}
            ]
        };

        let cart = [];
        let currentCategory = 'staple';
        let selectedTimeOption = 'now';
        let orderDateTime = null;

        // 切换分类
        function showCategory(category) {
            // 隐藏所有内容
            document.querySelectorAll('.category-content').forEach(content => {
                content.classList.remove('active');
            });
            
            // 移除所有标签的活动状态
            document.querySelectorAll('.category-tab').forEach(tab => {
                tab.classList.remove('active');
            });
            
            // 显示选中的内容
            document.getElementById(category).classList.add('active');
            
            // 激活选中的标签
            event.target.classList.add('active');
            
            currentCategory = category;
        }

        // 初始化菜单
        function initMenu() {
            Object.keys(menuData).forEach(category => {
                const grid = document.getElementById(category + 'Grid');
                grid.innerHTML = '';
                
                menuData[category].forEach(item => {
                    const menuItemHTML = `
                        <div class="menu-item">
                            <img src="${item.image}" alt="${item.name}" class="menu-item-image" onerror="this.src='data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iNDAwIiBoZWlnaHQ9IjMwMCIgdmlld0JveD0iMCAwIDQwMCAzMDAiIGZpbGw9Im5vbmUiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyI+CjxyZWN0IHdpZHRoPSI0MDAiIGhlaWdodD0iMzAwIiBmaWxsPSIjRjhGOUZBIi8+Cjx0ZXh0IHg9IjIwMCIgeT0iMTUwIiBmb250LWZhbWlseT0ic2Fucy1zZXJpZiIgZm9udC1zaXplPSIyNCIgZmlsbD0iIzdGOEM4RCIgdGV4dC1hbmNob3I9Im1pZGRsZSIgZG9taW5hbnQtYmFzZWxpbmU9Im1pZGRsZSI+JHtpdGVtLmljb259PC90ZXh0Pgo8L3N2Zz4K'">
                            <div class="menu-item-content">
                                <h3>${item.icon} ${item.name}</h3>
                                <div class="price">¥${item.price.toFixed(2)}</div>
                                <div class="description">${item.description}</div>
                                <div class="quantity-control">
                                    <button onclick="decreaseQuantity(${item.id})">-</button>
                                    <input type="number" class="quantity-input" id="quantity-${item.id}" value="1" min="1" max="99">
                                    <button onclick="increaseQuantity(${item.id})">+</button>
                                </div>
                                <button class="add-to-cart" onclick="addToCart(${item.id})">
                                    加入购物车
                                </button>
                            </div>
                        </div>
                    `;
                    grid.innerHTML += menuItemHTML;
                });
            });
        }

        // 获取菜品信息
        function getMenuItem(itemId) {
            for (let category in menuData) {
                const item = menuData[category].find(item => item.id === itemId);
                if (item) return item;
            }
            return null;
        }

        // 增加数量
        function increaseQuantity(itemId) {
            const quantityInput = document.getElementById(`quantity-${itemId}`);
            let quantity = parseInt(quantityInput.value);
            if (quantity < 99) {
                quantityInput.value = quantity + 1;
            }
        }

        // 减少数量
        function decreaseQuantity(itemId) {
            const quantityInput = document.getElementById(`quantity-${itemId}`);
            let quantity = parseInt(quantityInput.value);
            if (quantity > 1) {
                quantityInput.value = quantity - 1;
            }
        }

        // 添加到购物车
        function addToCart(itemId) {
            const item = getMenuItem(itemId);
            const quantity = parseInt(document.getElementById(`quantity-${itemId}`).value);
            
            const existingItem = cart.find(cartItem => cartItem.id === itemId);
            if (existingItem) {
                existingItem.quantity += quantity;
            } else {
                cart.push({
                    ...item,
                    quantity: quantity
                });
            }

            updateCart();
            
            // 重置数量为1
            document.getElementById(`quantity-${itemId}`).value = 1;
        }

        // 更新购物车显示
        function updateCart() {
            const cartItems = document.getElementById('cartItems');
            const cartCount = document.getElementById('cartCount');
            const totalAmount = document.getElementById('totalAmount');
            const submitButton = document.getElementById('submitOrder');

            if (cart.length === 0) {
                cartItems.innerHTML = `
                    <div class="empty-cart">
                        <p>购物车还是空的</p>
                        <p>快去选择您喜欢的菜品吧！</p>
                    </div>
                `;
                cartCount.textContent = '0';
                totalAmount.textContent = '0.00';
                submitButton.disabled = true;
                return;
            }

            let cartHTML = '';
            let total = 0;
            let totalItems = 0;

            cart.forEach((item, index) => {
                const itemTotal = item.price * item.quantity;
                total += itemTotal;
                totalItems += item.quantity;

                cartHTML += `
                    <div class="cart-item">
                        <div class="cart-item-info">
                            <div class="cart-item-name">${item.icon} ${item.name}</div>
                            <div class="cart-item-details">¥${item.price.toFixed(2)} × ${item.quantity}</div>
                        </div>
                        <div class="cart-item-price">¥${itemTotal.toFixed(2)}</div>
                        <button class="remove-btn" onclick="removeFromCart(${index})">删除</button>
                    </div>
                `;
            });

            cartItems.innerHTML = cartHTML;
            cartCount.textContent = totalItems;
            totalAmount.textContent = total.toFixed(2);
            submitButton.disabled = false;
        }

        // 从购物车移除商品
        function removeFromCart(index) {
            cart.splice(index, 1);
            updateCart();
        }

        // 清空购物车
        function clearCart() {
            cart = [];
            updateCart();
        }

        // 提交订单
        function submitOrder() {
            if (cart.length === 0) {
                alert('购物车为空，请先添加商品！');
                return;
            }

            // 验证预约时间
            if (selectedTimeOption === 'scheduled') {
                if (!orderDateTime) {
                    alert('请选择有效的预约时间！');
                    return;
                }
                
                const now = new Date();
                if (orderDateTime <= now) {
                    alert('预约时间不能是过去时间，请重新选择！');
                    return;
                }
            }

            let orderDetails = '🍽️ 订单详情：\n\n';
            let total = 0;

            cart.forEach(item => {
                const itemTotal = item.price * item.quantity;
                total += itemTotal;
                orderDetails += `${item.icon} ${item.name} × ${item.quantity} = ¥${itemTotal.toFixed(2)}\n`;
            });

            orderDetails += `\n💰 总计：¥${total.toFixed(2)}`;
            
            // 添加订单时间信息
            if (selectedTimeOption === 'now') {
                orderDetails += `\n⏰ 配送时间：立即下单 (预计30-45分钟内送达)`;
            } else {
                const formatDate = orderDateTime.toLocaleDateString('zh-CN', {
                    year: 'numeric',
                    month: 'long',
                    day: 'numeric',
                    weekday: 'long'
                });
                const formatTime = orderDateTime.toLocaleTimeString('zh-CN', {
                    hour: '2-digit',
                    minute: '2-digit'
                });
                orderDetails += `\n⏰ 预约时间：${formatDate} ${formatTime}`;
            }
            
            orderDetails += `\n📅 下单时间：${new Date().toLocaleString()}`;
            orderDetails += `\n🎉 订单编号：${Date.now()}`;

            let confirmMessage = orderDetails + '\n\n✅ 订单提交成功！感谢您的光临！';
            
            if (selectedTimeOption === 'now') {
                confirmMessage += '\n🚚 您的订单将在30-45分钟内送达';
            } else {
                confirmMessage += '\n📝 我们会按预约时间为您准备订单';
            }
            
            confirmMessage += '\n👨‍🍳 厨房正在为您精心准备...';

            alert(confirmMessage);
            
            // 清空购物车并重置时间选择
            clearCart();
            selectedTimeOption = 'now';
            document.querySelectorAll('.time-option').forEach(btn => {
                btn.classList.remove('active');
            });
            document.querySelector('.time-option').classList.add('active');
            document.getElementById('datetimeInputs').classList.remove('show');
            updateSelectedTime();
        }

        // 选择时间选项
        function selectTimeOption(option) {
            selectedTimeOption = option;
            
            // 更新按钮样式
            document.querySelectorAll('.time-option').forEach(btn => {
                btn.classList.remove('active');
            });
            event.target.classList.add('active');
            
            // 显示或隐藏日期时间输入
            const datetimeInputs = document.getElementById('datetimeInputs');
            if (option === 'scheduled') {
                datetimeInputs.classList.add('show');
                setDefaultDateTime();
            } else {
                datetimeInputs.classList.remove('show');
                updateSelectedTime();
            }
        }

        // 设置默认日期时间
        function setDefaultDateTime() {
            const now = new Date();
            const tomorrow = new Date(now);
            tomorrow.setDate(tomorrow.getDate() + 1);
            
            // 设置最早可选时间为明天
            const dateInput = document.getElementById('orderDate');
            const timeInput = document.getElementById('orderTime');
            
            dateInput.min = tomorrow.toISOString().split('T')[0];
            dateInput.value = tomorrow.toISOString().split('T')[0];
            
            // 设置默认时间为12:00
            timeInput.value = '12:00';
            
            updateSelectedTime();
        }

        // 更新选择的时间显示
        function updateSelectedTime() {
            const selectedTimeElement = document.getElementById('selectedTime');
            
            if (selectedTimeOption === 'now') {
                selectedTimeElement.textContent = '选择的时间：立即下单';
                orderDateTime = null;
            } else {
                const dateInput = document.getElementById('orderDate');
                const timeInput = document.getElementById('orderTime');
                
                if (dateInput.value && timeInput.value) {
                    const selectedDate = new Date(dateInput.value + 'T' + timeInput.value);
                    const now = new Date();
                    
                    // 验证选择的时间不能是过去时间
                    if (selectedDate <= now) {
                        alert('预约时间不能是过去时间，请选择未来的时间！');
                        setDefaultDateTime();
                        return;
                    }
                    
                    const formatDate = selectedDate.toLocaleDateString('zh-CN', {
                        year: 'numeric',
                        month: 'long',
                        day: 'numeric',
                        weekday: 'long'
                    });
                    const formatTime = selectedDate.toLocaleTimeString('zh-CN', {
                        hour: '2-digit',
                        minute: '2-digit'
                    });
                    
                    selectedTimeElement.textContent = `预约时间：${formatDate} ${formatTime}`;
                    orderDateTime = selectedDate;
                } else {
                    selectedTimeElement.textContent = '请选择日期和时间';
                    orderDateTime = null;
                }
            }
        }

        // 页面加载完成后初始化菜单
        document.addEventListener('DOMContentLoaded', function() {
            initMenu();
            
            // 初始化时间选择
            updateSelectedTime();
        });
    </script>
</body>
</html> 
