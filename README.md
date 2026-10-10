<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Trabalho Faculdade</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
    <style>
        body {
            background-color: #000000;
            color: #ffffff;
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
            margin: 0;
            padding: 0;
            -webkit-tap-highlight-color: transparent;
        }

        .app-container {
            width: 100%;
            height: 100vh;
            display: flex;
            flex-direction: column;
            position: relative;
            overflow: hidden;
        }

        ::-webkit-scrollbar { display: none; }
        .escondido { display: none !important; }

        /* Animação da linha de carregamento */
        @keyframes scanline {
            0% { transform: translateX(-100%); }
            100% { transform: translateX(200%); }
        }
        .animated-line-container { width: 100%; height: 4px; background-color: #002dd1; position: relative; overflow: hidden; }
        .animated-line {
            position: absolute; top: 0; left: 0; height: 100%; width: 50%;
            background: linear-gradient(90deg, transparent, #00ffcc, #00b38f, transparent);
            animation: scanline 1.5s infinite linear;
        }
        .qr-placeholder {
            background-image: repeating-linear-gradient(45deg, #000 25%, transparent 25%, transparent 75%, #000 75%, #000), repeating-linear-gradient(45deg, #000 25%, #fff 25%, #fff 75%, #000 75%, #000);
            background-position: 0 0, 4px 4px; background-size: 8px 8px;
        }

        /* Tela do Ingresso que desliza por cima */
        .ticket-overlay {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background-color: #121212; z-index: 50;
            transform: translateX(100%); transition: transform 0.3s ease;
            overflow-y: auto; display: flex; flex-direction: column;
        }
        .ticket-overlay.ativo { transform: translateX(0); }
    </style>
</head>
<body>

    <div class="app-container">
        
        <!-- ==========================================
             TELA 1: EXPLORE (Meus Ingressos)
             ========================================== -->
        <div id="view-explore" class="flex-1 flex flex-col h-full w-full">
            <header class="flex justify-between items-center px-5 pt-8 pb-4">
                <h1 class="text-[26px] font-extrabold tracking-tight">Meus ingressos</h1>
                <div class="flex items-center gap-6">
                    <span class="material-icons text-gray-400 text-[26px]">notifications_none</span>
                    <span class="material-icons text-gray-400 text-[26px]">person_outline</span>
                </div>
            </header>

            <div class="px-5 py-2">
                <div class="flex bg-[#1c1c1e] rounded-xl p-1">
                    <button class="flex-1 py-2 text-[15px] font-semibold bg-white text-black rounded-lg shadow-sm">Próximos</button>
                    <button class="flex-1 py-2 text-[15px] font-semibold text-gray-400">Anterior</button>
                </div>
            </div>

            <div class="flex-1 overflow-y-auto px-5 py-6 pb-24">
                <!-- Cartão Clicável -->
                <div onclick="abrirTicket()" class="bg-[#1c1c1e] rounded-[24px] overflow-hidden cursor-pointer shadow-lg active:scale-[0.98] transition-transform">
                    <div class="relative h-[220px] bg-gray-800 flex items-center justify-center overflow-hidden">
                        <!-- Imagem da formatura -->
                        <img src="zayn.jpeg" alt="Zayn" class="absolute inset-0 w-full h-full object-cover">
                        <div class="absolute bottom-4 left-4">
                            <span class="bg-[#00e6c3] text-black text-[11px] font-bold px-2 py-1 rounded">AGORA</span>
                        </div>
                    </div>

                    <div class="p-5">
                        <div class="flex items-center gap-2 mb-1.5">
                            <span class="text-[#00e6c3] text-[13px] font-semibold">2 ingressos</span>
                            <span class="text-gray-400 text-[13px]">Sábado 10 20:00hs</span>
                        </div>
                        <h3 class="text-white text-[18px] font-bold leading-tight mb-1">ZAYN: The Konnakol Tour - São Paulo</h3>
                        <p class="text-gray-400 text-[14px]">Nubank Parque</p>
                    </div>
                </div>
            </div>
        </div>

        <!-- ==========================================
             TELA 2: PERFIL
             ========================================== -->
        <div id="view-perfil" class="escondido flex-1 flex flex-col h-full w-full">
            <header class="flex justify-between items-center px-5 pt-8 pb-4 border-b border-gray-800">
                <h1 class="text-[26px] font-extrabold tracking-tight">Meu Perfil</h1>
                <span class="material-icons text-gray-400 text-[26px]">settings</span>
            </header>

            <div class="flex-1 overflow-y-auto px-5 py-8 pb-24 flex flex-col items-center">
                <div class="w-24 h-24 bg-gray-800 rounded-full flex items-center justify-center mb-4 shadow-lg border-2 border-gray-700 overflow-hidden">
                    <img src="formatura.png" alt="Foto Perfil" class="w-full h-full object-cover">
                </div>
                
                <h2 class="text-white text-[22px] font-bold mb-1">Stefanne Fonseca</h2>
                <p class="text-gray-400 text-[14px] mb-8">stefanne.fonseca94@gmail.com</p>

                <div class="w-full bg-[#1c1c1e] rounded-[16px] overflow-hidden shadow-lg">
                    <button class="w-full flex items-center justify-between p-4 border-b border-gray-800 hover:bg-gray-800 transition-colors">
                        <div class="flex items-center gap-3">
                            <span class="material-icons text-gray-400">account_circle</span>
                            <span class="text-[15px] font-medium text-white">Dados Pessoais</span>
                        </div>
                        <span class="material-icons text-gray-500">chevron_right</span>
                    </button>
                    <button class="w-full flex items-center justify-between p-4 hover:bg-gray-800 transition-colors">
                        <div class="flex items-center gap-3">
                            <span class="material-icons text-red-500">logout</span>
                            <span class="text-[15px] font-medium text-red-500">Sair da conta</span>
                        </div>
                    </button>
                </div>
            </div>
        </div>

        <!-- ==========================================
             MENU INFERIOR FIXO
             ========================================== -->
        <nav class="absolute bottom-0 w-full bg-white border-t border-gray-200 flex justify-around items-center h-[65px] z-20">
            <a href="#" onclick="mudarTela('explore', this)" class="nav-btn flex flex-col items-center text-yellow-500 w-full py-2">
                <span class="material-icons text-[26px]">home</span>
                <span class="text-[11px] font-semibold mt-1">Explore</span>
            </a>
            <a href="#" class="nav-btn flex flex-col items-center text-gray-400 w-full py-2">
                <span class="material-icons text-[26px]">search</span>
                <span class="text-[11px] font-semibold mt-1">Buscar</span>
            </a>
            <a href="#" class="nav-btn flex flex-col items-center text-gray-400 w-full py-2">
                <span class="material-icons text-[26px]">confirmation_number</span>
                <span class="text-[11px] font-semibold mt-1">Meus Eventos</span>
            </a>
            <a href="#" onclick="mudarTela('perfil', this)" class="nav-btn flex flex-col items-center text-gray-400 hover:text-gray-900 transition-colors w-full py-2">
                <span class="material-icons text-[26px]">person</span>
                <span class="text-[11px] font-semibold mt-1">Perfil</span>
            </a>
        </nav>

        <!-- ==========================================
             TELA 3: INGRESSO ABERTO (SOBREPOSIÇÃO)
             ========================================== -->
        <div id="view-ticket" class="ticket-overlay">
            <header class="sticky top-0 z-20 bg-[#121212]/95 backdrop-blur-sm px-4 pt-12 pb-3 flex items-center justify-between border-b border-gray-800">
                <button onclick="fecharTicket()" class="p-2 -ml-2 text-gray-300 hover:text-white transition-colors">
                    <span class="material-icons">arrow_back_ios_new</span>
                </button>
                <div class="flex-1 text-center px-2">
                    <h2 class="text-white text-sm font-bold truncate">ZAYN: The Konnakol Tour - São Paulo</h2>
                    <p class="text-gray-400 text-[11px]">10/10/26 - Nubank Parque</p>
                </div>
                <button class="p-2 -mr-2 text-gray-300 hover:text-white">
                    <span class="material-icons">ios_share</span>
                </button>
            </header>

            <div class="px-4 py-4 pb-12 flex-1">
                <div class="w-full flex gap-2">
                    <div class="flex-1 rounded-2xl overflow-hidden shadow-2xl bg-white flex flex-col">
                        <div class="w-full bg-gray-900 relative overflow-hidden">
    <img src="banner-topo.jpeg" alt="Topo do Ingresso" class="w-full h-auto object-cover">
</div>

                        <!-- BARRA DE CARREGAMENTO ANIMADA -->
                        <div class="animated-line-container">
                            <div class="animated-line"></div>
                        </div>

                        <div class="p-4 flex flex-row items-center justify-between bg-[#f5f7fa]">
                           <div class="w-24 h-24 bg-white p-1 rounded border border-gray-200 shadow-sm flex items-center justify-center overflow-hidden">
    <img src="qrcode.png" alt="Código QR" class="w-full h-full object-cover">
</div>
                            <div class="flex-1 pl-4 flex flex-col justify-center">
                                <div class="mb-3">
                                    <p class="text-gray-500 text-[10px] font-bold uppercase tracking-wider mb-0.5">SETOR</p>
                                    <p class="text-black font-bold text-sm">Pista Premium</p>
                                </div>
                                <div class="mb-3">
                                    <p class="text-gray-500 text-[10px] font-bold uppercase tracking-wider mb-0.5">ACESSO</p>
                                    <p class="text-black font-bold text-sm">Portão B</p>
                                </div>
                                <button class="bg-[#e2e8f0] text-gray-700 text-xs font-semibold py-1.5 px-3 rounded-lg w-full mt-1">
                                    Mais informação
                                </button>
                            </div>
                        </div>

                        <div class="h-[1px] w-full bg-gray-300"></div>

                        <div class="p-4 bg-[#eceeec] flex flex-col gap-4">
                            <div>
                                <p class="text-gray-500 text-[10px] font-bold uppercase tracking-wider mb-0.5">TAXA</p>
                                <p class="text-gray-800 font-bold text-sm">Inteira - R$ 890</p>
                            </div>
                            <div class="grid grid-cols-2 gap-4">
                                <div>
                                    <p class="text-gray-500 text-[10px] font-bold uppercase tracking-wider mb-0.5">SEÇÃO</p>
                                    <p class="text-gray-800 font-bold text-sm uppercase">PISTA PREMIUM</p>
                                </div>
                                <div>
                                    <p class="text-gray-500 text-[10px] font-bold uppercase tracking-wider mb-0.5">FILEIRA</p>
                                    <p class="text-gray-800 font-bold text-sm">Não numerado</p>
                                </div>
                            </div>
                            <div class="grid grid-cols-2 gap-4">
                                <div>
                                    <p class="text-gray-500 text-[10px] font-bold uppercase tracking-wider mb-0.5">ABERTURA</p>
                                    <p class="text-gray-800 font-bold text-sm">16:00</p>
                                </div>
                                <div>
                                    <p class="text-gray-500 text-[10px] font-bold uppercase tracking-wider mb-0.5">INÍCIO</p>
                                    <p class="text-gray-800 font-bold text-sm">20:00</p>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

    </div>

    <script>
        // Função para alternar entre as abas do menu inferior
        function mudarTela(telaAlvo, elementoClicado) {
            document.getElementById('view-explore').classList.add('escondido');
            document.getElementById('view-perfil').classList.add('escondido');
            
            document.getElementById('view-' + telaAlvo).classList.remove('escondido');

            let botoes = document.querySelectorAll('.nav-btn');
            botoes.forEach(function(botao) {
                botao.classList.remove('text-yellow-500');
                botao.classList.add('text-gray-400');
            });

            elementoClicado.classList.remove('text-gray-400');
            elementoClicado.classList.add('text-yellow-500');
        }

        // Funções para abrir e fechar a tela do ingresso
        function abrirTicket() {
            document.getElementById('view-ticket').classList.add('ativo');
        }

        function fecharTicket() {
            document.getElementById('view-ticket').classList.remove('ativo');
        }
    </script>
</body>
</html>

<img width="640" height="640" alt="zayn" src="https://github.com/user-attachments/assets/18393c86-2faa-42c2-a34a-96e6a5a6572c" />
<img width="902" height="901" alt="qrcode" src="https://github.com/user-attachments/assets/e8cbc5ac-aa7c-4196-bfce-a18cc24aeeb7" />
<img width="1473" height="1068" alt="banner-topo" src="https://github.com/user-attachments/assets/1394e1c8-f5dc-4344-a92f-a829d6a72b61" />
