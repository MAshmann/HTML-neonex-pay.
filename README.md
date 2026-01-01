<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Neonex Pay | Official Web3 Infrastructure</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/ethers/5.7.2/ethers.umd.min.js"></script>
    <style>
        :root { --neon-gold: #FFD700; --bg-dark: #000000; }
        body { background-color: var(--bg-dark); color: white; font-family: 'Inter', sans-serif; }
        .glass { background: rgba(255, 255, 255, 0.03); backdrop-filter: blur(12px); border: 1px solid rgba(255, 255, 255, 0.1); }
        .neon-glow { box-shadow: 0 0 20px rgba(255, 215, 0, 0.3); }
    </style>
</head>
<body>

    <nav class="fixed w-full z-50 glass px-6 py-4 flex justify-between items-center">
        <div class="text-2xl font-black italic text-yellow-400 tracking-tighter">NEONEX</div>
        <button onclick="connectWallet()" id="walletBtn" class="text-[10px] font-bold border border-yellow-400/50 px-4 py-2 rounded-full hover:bg-yellow-400 hover:text-black transition-all">CONECTAR CARTEIRA</button>
    </nav>

    <section class="pt-32 pb-16 px-6 text-center">
        <h1 class="text-5xl font-black mb-6 leading-[1.1]">Pagamentos Web3 <br><span class="text-yellow-400">Sem Fronteiras.</span></h1>
        <p class="text-zinc-500 max-w-sm mx-auto text-sm mb-10">A infraestrutura completa para o Brasil: Pix + Blockchain com taxas próximas de zero.</p>
        <div class="flex justify-center gap-4">
            <a href="#pagar" class="bg-yellow-400 text-black px-8 py-4 rounded-2xl font-black uppercase text-sm neon-glow">Usar Agora</a>
        </div>
    </section>

    <section id="pagar" class="py-12 px-6">
        <div class="max-w-md mx-auto glass p-8 rounded-[2.5rem] border-2 border-yellow-400/10">
            <h2 class="text-center font-bold text-zinc-400 uppercase text-xs tracking-widest mb-6">Terminal de Transação</h2>
            <div class="bg-black/50 p-6 rounded-3xl mb-4 border border-zinc-800">
                <input id="amountInput" type="number" placeholder="0.00" class="w-full bg-transparent text-4xl text-center font-bold text-yellow-400 outline-none">
                <span class="block text-center text-zinc-600 text-[10px] mt-2 font-bold uppercase tracking-widest">Valor em POL (Polygon)</span>
            </div>
            <button onclick="executePayment()" class="w-full bg-white text-black py-5 rounded-2xl font-black text-lg hover:bg-yellow-400 transition-all uppercase tracking-tighter">Confirmar Pagamento</button>
            <p id="statusTxt" class="text-center mt-4 text-[10px] text-zinc-500 font-mono italic">Aguardando interação...</p>
        </div>
    </section>

    <section class="py-12 px-6 grid grid-cols-2 gap-4 max-w-md mx-auto">
        <div class="glass p-4 rounded-2xl text-center">
            <div class="text-yellow-400 font-bold text-lg">AES-256</div>
            <div class="text-zinc-600 text-[9px] uppercase">Criptografia</div>
        </div>
        <div class="glass p-4 rounded-2xl text-center">
            <div class="text-yellow-400 font-bold text-lg">P2P</div>
            <div class="text-zinc-600 text-[9px] uppercase">Não-Custodial</div>
        </div>
    </section>

    <section class="py-10 px-8 text-zinc-700 text-[10px] leading-relaxed max-w-2xl mx-auto border-t border-zinc-900">
        <h4 class="font-bold text-zinc-500 mb-2 uppercase">Termos e Privacidade</h4>
        <p>Ao conectar sua carteira, você concorda com o processamento descentralizado na rede Polygon. A Neonex Pay não armazena chaves privadas. Todas as transações são finais e regidas pelos Smart Contracts da plataforma. Compatível com LGPD e normas internacionais de ativos digitais.</p>
    </section>

    <footer class="py-12 text-center text-zinc-600 text-[9px] uppercase tracking-[0.3em]">
        Neonex Pay &copy; 2026 | Built for the New Economy
    </footer>

    <script>
        async function connectWallet() {
            if (window.ethereum) {
                const accounts = await window.ethereum.request({ method: 'eth_requestAccounts' });
                document.getElementById('walletBtn').innerText = accounts[0].substring(0,6) + "..." + accounts[0].substring(38);
                document.getElementById('walletBtn').classList.add('bg-green-500/10', 'text-green-500');
            }
        }

        async function executePayment() {
            if (!window.ethereum) return alert("Use o navegador da MetaMask!");
            const provider = new ethers.providers.Web3Provider(window.ethereum);
            const signer = provider.getSigner();
            const val = document.getElementById('amountInput').value || "0.01";
            
            try {
                document.getElementById('statusTxt').innerText = "Processando Segurança...";
                const tx = await signer.sendTransaction({
                    to: "SEU_ENDEREÇO_AQUI", // Coloque sua carteira aqui
                    value: ethers.utils.parseEther(val)
                });
                document.getElementById('statusTxt').innerText = "Sucesso! Hash: " + tx.hash.substring(0,12);
            } catch (err) {
                document.getElementById('statusTxt').innerText = "Erro: " + err.message.substring(0,25);
            }
        }
    </script>
</body>
</html>
# HTML-neonex-pay.
