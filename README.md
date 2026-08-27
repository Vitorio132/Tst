<html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Burguer & Cia - App de Pedidos</title>
    
    <!-- Configurações PWA Unificadas -->
    <meta name="theme-color" content="#ea580c">
    <meta name="mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <meta name="apple-mobile-web-app-title" content="Burguer & Cia">
    <link rel="apple-touch-icon" href="https://cdn-icons-png.flaticon.com/512/3075/3075977.png">
    
  <!-- Manifest embutido diretamente via Data URI -->
    <link rel="manifest" href='data:application/json,{"name":"Burguer %26 Cia - App de Pedidos","short_name":"Burguer %26 Cia","description":"Faça seu pedido diretamente pelo nosso aplicativo!","start_url":"./","display":"standalone","background_color":"%230c0a09","theme_color":"%23ea580c","icons":[{"src":"https://cdn-icons-png.flaticon.com/512/3075/3075977.png","sizes":"192x192","type":"image/png"},{"src":"https://cdn-icons-png.flaticon.com/512/3075/3075977.png","sizes":"512x512","type":"image/png"}]}'>

    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: #0c0a09;
            background-image: 
                linear-gradient(rgba(12, 10, 9, 0.9), rgba(12, 10, 9, 0.9)), 
                url('https://images.unsplash.com/photo-1555396273-367ea4eb4db5?w=1200');
            background-position: center;
            background-size: cover;
            background-attachment: fixed;
            color: #f8fafc;
            padding-bottom: 90px;
        }

        header {
            background-color: rgba(28, 25, 23, 0.95);
            backdrop-filter: blur(8px);
            padding: 20px;
            text-align: center;
            border-bottom: 2px solid #ea580c;
            position: sticky;
            top: 0;
            z-index: 100;
        }

        header h1 {
            color: #f97316;
            font-size: 1.5rem;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        header p {
            color: #a8a29e;
            font-size: 0.85rem;
            margin-top: 2px;
        }

        .container {
            max-width: 500px;
            margin: 0 auto;
            padding: 15px;
        }

        .hero-banner {
            background: linear-gradient(135deg, #ea580c, #9a3412);
            border-radius: 16px;
            padding: 20px;
            text-align: center;
            margin-bottom: 20px;
            box-shadow: 0 4px 15px rgba(234, 88, 12, 0.3);
        }

        .hero-banner h2 {
            font-size: 1.3rem;
            color: #fff;
            margin-bottom: 6px;
        }

        .hero-banner p {
            font-size: 0.85rem;
            color: #ffedd5;
        }

        .categorias-bar {
            display: flex;
            gap: 10px;
            overflow-x: auto;
            padding-bottom: 10px;
            margin-bottom: 20px;
            scrollbar-width: none;
        }

        .categorias-bar::-webkit-scrollbar {
            display: none;
        }

        .btn-categoria {
            background-color: rgba(28, 25, 23, 0.9);
            border: 1px solid #44403c;
            color: #d6d3d1;
            padding: 8px 16px;
            border-radius: 20px;
            font-size: 0.85rem;
            font-weight: bold;
            white-space: nowrap;
            cursor: pointer;
            transition: all 0.2s;
        }

        .btn-categoria.active {
            background-color: #ea580c;
            color: #fff;
            border-color: #ea580c;
        }

        .secao-titulo {
            font-size: 1.1rem;
            margin-bottom: 15px;
            color: #f3f4f6;
        }

        .card-produto {
            background-color: rgba(28, 25, 23, 0.9);
            border: 1px solid #44403c;
            border-radius: 14px;
            padding: 15px;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 15px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.3);
            backdrop-filter: blur(4px);
        }

        .card-produto.destaque {
            border: 1px solid #f97316;
            background: linear-gradient(180deg, rgba(43, 33, 24, 0.9), rgba(28, 25, 23, 0.9));
        }

        .badge-combo {
            background-color: #ea580c;
            color: #fff;
            font-size: 0.65rem;
            font-weight: bold;
            padding: 2px 6px;
            border-radius: 4px;
            text-transform: uppercase;
            display: inline-block;
            margin-bottom: 4px;
        }

        .card-produto img {
            width: 85px;
            height: 85px;
            border-radius: 10px;
            object-fit: cover;
            background-color: #292524;
            border: 1px solid #57534e;
        }

        .detalhes-produto {
            flex: 1;
        }

        .detalhes-produto h3 {
            font-size: 1rem;
            color: #f8fafc;
            margin-bottom: 4px;
        }

        .detalhes-produto p {
            font-size: 0.8rem;
            color: #a8a29e;
            margin-bottom: 8px;
            line-height: 1.2;
        }

        .preco {
            color: #f97316;
            font-weight: bold;
            font-size: 1.05rem;
        }

        .btn-add {
            background-color: #ea580c;
            color: white;
            border: none;
            padding: 8px 14px;
            border-radius: 8px;
            font-weight: bold;
            font-size: 0.85rem;
            cursor: pointer;
        }

        .cart-bar {
            position: fixed;
            bottom: 0;
            left: 0;
            right: 0;
            background-color: rgba(28, 25, 23, 0.98);
            border-top: 1px solid #44403c;
            padding: 15px 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            max-width: 500px;
            margin: 0 auto;
            backdrop-filter: blur(10px);
        }

        .total-info p {
            font-size: 0.8rem;
            color: #a8a29e;
        }

        .total-info span {
            font-size: 1.25rem;
            font-weight: bold;
            color: #22c55e;
        }

        .btn-enviar {
            background-color: #22c55e;
            color: white;
            padding: 12px 22px;
            border-radius: 25px;
            font-weight: bold;
            font-size: 0.95rem;
            border: none;
            cursor: pointer;
        }

        .modal-overlay {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.85);
            z-index: 1000;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .modal-overlay.active {
            display: flex;
        }

        .modal-content {
            background-color: #1c1917;
            border: 1px solid #44403c;
            border-radius: 16px;
            width: 100%;
            max-width: 450px;
            padding: 25px;
        }

        .form-group {
            margin-bottom: 15px;
            text-align: left;
        }

        .form-group label {
            display: block;
            font-size: 0.85rem;
            color: #d6d3d1;
            margin-bottom: 6px;
        }

        .form-group input, .form-group select {
            width: 100%;
            padding: 10px 12px;
            background-color: #0c0a09;
            border: 1px solid #44403c;
            border-radius: 8px;
            color: #f8fafc;
            font-size: 0.9rem;
            outline: none;
        }

        .modal-buttons {
            display: flex;
            gap: 10px;
            margin-top: 20px;
        }

        .btn-cancelar {
            background-color: #292524;
            color: #d6d3d1;
            border: none;
            padding: 12px;
            border-radius: 8px;
            font-weight: bold;
            flex: 1;
            cursor: pointer;
        }

        .btn-confirmar {
            background-color: #22c55e;
            color: white;
            border: none;
            padding: 12px;
            border-radius: 8px;
            font-weight: bold;
            flex: 2;
            cursor: pointer;
        }

        .success-icon {
            font-size: 3rem;
            color: #22c55e;
            margin-bottom: 10px;
            text-align: center;
        }
    </style>
</head>
<body>

    <header>
        <h1 id="nome-loja">🍔 Burguer & Cia</h1>
        <p>Os melhores lanches da cidade na sua casa</p>
    </header>

    <div class="container">
        <div class="hero-banner">
            <h2>Sabor Artesanal Incomparável! 🔥</h2>
            <p>Ingredientes selecionados, carnes suculentas e entrega rápida.</p>
        </div>

        <div class="categorias-bar">
            <button class="btn-categoria active" onclick="filtrarCategoria('todos', this)">🔥 Todos</button>
            <button class="btn-categoria" onclick="filtrarCategoria('combos', this)">⚡ Combos</button>
            <button class="btn-categoria" onclick="filtrarCategoria('sanduiches', this)">🍔 Sanduíches</button>
            <button class="btn-categoria" onclick="filtrarCategoria('batatas', this)">🍟 Batatas Fritas</button>
            <button class="btn-categoria" onclick="filtrarCategoria('bebidas', this)">🥤 Bebidas</button>
        </div>

        <h2 class="secao-titulo" id="titulo-categoria">Nosso Cardápio</h2>
        <div id="lista-produtos"></div>
    </div>

    <div class="cart-bar">
        <div class="total-info">
            <p>Total do Pedido (<span id="qtd-itens">0</span> itens):</p>
            <span id="valor-total">R$ 0,00</span>
        </div>
        <button onclick="abrirModal()" class="btn-enviar">Finalizar Pedido</button>
    </div>

    <!-- Modal Formulario -->
    <div class="modal-overlay" id="modal-checkout">
        <div class="modal-content">
            <h2 style="color: #f97316; margin-bottom: 15px; text-align: left;">🛵 Dados para Entrega</h2>
            
            <div class="form-group">
                <label for="cliente-nome">Seu Nome *</label>
                <input type="text" id="cliente-nome" placeholder="Digite seu nome completo">
            </div>

            <div class="form-group">
                <label for="cliente-endereco">Endereço de Entrega *</label>
                <input type="text" id="cliente-endereco" placeholder="Rua, número, bairro e complemento">
            </div>

            <div class="form-group">
                <label for="cliente-pagamento">Forma de Pagamento *</label>
                <select id="cliente-pagamento">
                    <option value="Pix">Pix</option>
                    <option value="Cartão de Crédito">Cartão de Crédito</option>
                    <option value="Cartão de Débito">Cartão de Débito</option>
                    <option value="Dinheiro">Dinheiro</option>
                </select>
            </div>

            <div class="modal-buttons">
                <button onclick="fecharModal()" class="btn-cancelar">Voltar</button>
                <button onclick="confirmarEnviarWhatsApp()" class="btn-confirmar">Enviar Pedido</button>
            </div>
        </div>
    </div>

    <!-- Modal Sucesso -->
    <div class="modal-overlay" id="modal-sucesso">
        <div class="modal-content" style="text-align: center;">
            <div class="success-icon">✓</div>
            <h2 style="color: #22c55e; margin-bottom: 10px;">Pedido Confirmado!</h2>
            <p style="color: #d6d3d1; font-size: 0.95rem; margin-bottom: 20px;">
                Seu pedido foi registrado com sucesso e será entregue em breve no seu endereço!
            </p>
            <button onclick="fecharSucesso()" class="btn-confirmar" style="width: 100%;">Entendido</button>
        </div>
    </div>

    <script>
        // Registra o Service Worker dinamicamente sem precisar de outro arquivo JS
        if ('serviceWorker' in navigator) {
            const swCode = `
                self.addEventListener('install', e => self.skipWaiting());
                self.addEventListener('fetch', e => e.respondWith(fetch(e.request)));
            `;
            const blob = new Blob([swCode], { type: 'application/javascript' });
            const swUrl = URL.createObjectURL(blob);
            navigator.serviceWorker.register(swUrl).catch(err => console.log('SW Error:', err));
        }

        const SEU_WHATSAPP = "5500999999999"; 

        const produtos = [
            {
                id: 1,
                categoria: "combos",
                nome: "Combo Casal Supremo",
                descricao: "2 Monster Burguers + 1 Batata Grande + 1 Refrigerante 1L.",
                preco: 69.90,
                imagem: "https://images.unsplash.com/photo-1550547660-d9450f859349?w=200",
                destaque: true
            },
            {
                id: 2,
                categoria: "combos",
                nome: "Combo Individual Smash",
                descricao: "1 Smash Burguer + 1 Batata Rústica Pequena + 1 Lata.",
                preco: 38.00,
                imagem: "https://images.unsplash.com/photo-1594212699903-ec8a3eca50f6?w=200",
                destaque: true
            },
            {
                id: 3,
                categoria: "sanduiches",
                nome: "Monster Burguer",
                descricao: "Pão brioche, 2 hambúrgueres 180g, duplo cheddar e bacon.",
                preco: 34.90,
                imagem: "https://images.unsplash.com/photo-1568901346375-23c9450c58cd?w=200",
                destaque: false
            },
            {
                id: 4,
                categoria: "sanduiches",
                nome: "Smash Bacon Classic",
                descricao: "Pão, carne smash 100g, queijo prato, molho da casa e bacon.",
                preco: 24.90,
                imagem: "https://images.unsplash.com/photo-1586190848861-99aa4a171e90?w=200",
                destaque: false
            },
            {
                id: 5,
                categoria: "batatas",
                nome: "Batata Rústica Bacon",
                descricao: "Batatas crocantes cobertas com cheddar cremoso e bacon em cubos.",
                preco: 22.00,
                imagem: "https://images.unsplash.com/photo-1573080496219-bb080dd4f877?w=200",
                destaque: false
            },
            {
                id: 6,
                categoria: "batatas",
                nome: "Batata Frita Tradicional",
                descricao: "Porção de batata palito bem crocante e sequinha.",
                preco: 15.00,
                imagem: "https://images.unsplash.com/photo-1541592106381-b31e9677c0e5?w=200",
                destaque: false
            },
            {
                id: 7,
                categoria: "bebidas",
                nome: "Milkshake de Chocolate",
                descricao: "Copão 500ml com calda especial de chocolate.",
                preco: 16.50,
                imagem: "https://images.unsplash.com/photo-1572490122747-3968b75cc699?w=200",
                destaque: false
            },
            {
                id: 8,
                categoria: "bebidas",
                nome: "Coca-Cola Lata 350ml",
                descricao: "Lata trincando de gelada.",
                preco: 6.00,
                imagem: "https://images.unsplash.com/photo-1622483767028-3f66f32aef97?w=200",
                destaque: false
            }
        ];

        let carrinho = [];

        function renderizarProdutos(categoriaFiltro = 'todos') {
            const container = document.getElementById('lista-produtos');
            container.innerHTML = "";

            const produtosFiltrados = categoriaFiltro === 'todos' 
                ? produtos 
                : produtos.filter(p => p.categoria === categoriaFiltro);

            produtosFiltrados.forEach(produto => {
                const classeDestaque = produto.destaque ? 'destaque' : '';
                const tagCombo = produto.destaque ? `<span class="badge-combo">Oferta Combo</span><br>` : '';

                container.innerHTML += `
                    <div class="card-produto ${classeDestaque}">
                        <img src="${produto.imagem}" alt="${produto.nome}">
                        <div class="detalhes-produto">
                            ${tagCombo}
                            <h3>${produto.nome}</h3>
                            <p>${produto.descricao}</p>
                            <span class="preco">R$ ${produto.preco.toFixed(2).replace('.', ',')}</span>
                        </div>
                        <button class="btn-add" onclick="adicionarAoCarrinho(${produto.id})">+ Add</button>
                    </div>
                `;
            });
        }

        function filtrarCategoria(categoria, elemento) {
            document.querySelectorAll('.btn-categoria').forEach(btn => btn.classList.remove('active'));
            elemento.classList.add('active');
            
            const nomesTitulos = {
                'todos': 'Nosso Cardápio Completo',
                'combos': '⚡ Combos Promocionais',
                'sanduiches': '🍔 Sanduíches Artesanais',
                'batatas': '🍟 Batatas Fritas & Porções',
                'bebidas': '🥤 Bebidas & Shakes'
            };

            document.getElementById('titulo-categoria').innerText = nomesTitulos[categoria] || 'Nosso Cardápio';
            renderizarProdutos(categoria);
        }

        function adicionarAoCarrinho(id) {
            const produto = produtos.find(p => p.id === id);
            carrinho.push(produto);
            atualizarCarrinho();
        }

        function atualizarCarrinho() {
            document.getElementById('qtd-itens').innerText = carrinho.length;
            const total = carrinho.reduce((acc, item) => acc + item.preco, 0);
            document.getElementById('valor-total').innerText = `R$ ${total.toFixed(2).replace('.', ',')}`;
        }

        function abrirModal() {
            if (carrinho.length === 0) {
                alert("Seu carrinho está vazio!");
                return;
            }
            document.getElementById('modal-checkout').classList.add('active');
        }

        function fecharModal() {
            document.getElementById('modal-checkout').classList.remove('active');
        }

        function fecharSucesso() {
            document.getElementById('modal-sucesso').classList.remove('active');
            carrinho = [];
            atualizarCarrinho();
            document.getElementById('cliente-nome').value = "";
            document.getElementById('cliente-endereco').value = "";
        }

        function confirmarEnviarWhatsApp() {
            const nome = document.getElementById('cliente-nome').value.trim();
            const endereco = document.getElementById('cliente-endereco').value.trim();
            const pagamento = document.getElementById('cliente-pagamento').value;

            if (!nome || !endereco) {
                alert("Por favor, preencha seu nome e endereço.");
                return;
            }

            let mensagem = `*Novo Pedido - Burguer & Cia*\n\n`;
            mensagem += `*Cliente:* ${nome}\n`;
            mensagem += `*Endereço:* ${endereco}\n`;
            mensagem += `*Pagamento:* ${pagamento}\n\n`;
            mensagem += `*Itens do Pedido:*\n`;
            
            let total = 0;
            carrinho.forEach((item, index) => {
                mensagem += `${index + 1}. ${item.nome} - R$ ${item.preco.toFixed(2).replace('.', ',')}\n`;
                total += item.preco;
            });

            mensagem += `\n*Total a pagar:* R$ ${total.toFixed(2).replace('.', ',')}`;

            const url = `https://wa.me/${5592986025704}?text=${encodeURIComponent(mensagem)}`;
            window.open(url, '_blank');

            fecharModal();
            document.getElementById('modal-sucesso').classList.add('active');
        }

        renderizarProdutos();
    </script>
</body>
</html>
