import Header from "@/components/Header";
import Sidebar from "@/components/Sidebar";
import BalanceCard from "@/components/BalanceCard";
import PixNeoCard from "@/components/PixNeoCard";
import WalletCard from "@/components/WalletCard";
import TransactionsList from "@/components/TransactionsList";
import NetworkStatus from "@/components/NetworkStatus";

export default function Dashboard() {
  return (
    <div className="flex h-screen bg-black text-yellow-400">
      <Sidebar />

      <div className="flex-1 flex flex-col">
        <Header user="Marcelo" />

        <main className="p-4 grid grid-cols-1 md:grid-cols-3 gap-4">
          <BalanceCard />
          <PixNeoCard />
          <WalletCard />

          <div className="md:col-span-2">
            <TransactionsList />
          </div>

          <NetworkStatus />
        </main>
      </div>
    </div>
  );
}

import { ShieldCheck } from "lucide-react";

export default function Header({ user }: { user: string }) {
  return (
    <header className="flex items-center justify-between px-6 py-4 border-b border-yellow-500/20">
      <h1 className="text-xl font-bold tracking-widest">NEONEX-PAY</h1>

      <div className="flex items-center gap-3">
        <ShieldCheck className="text-yellow-400" />
        <span className="text-sm">Olá, {user}</span>
      </div>
    </header>
  );
}
import { LayoutDashboard, Wallet, Repeat, Settings } from "lucide-react";

const menu = [
  { name: "Dashboard", icon: LayoutDashboard },
  { name: "Wallet", icon: Wallet },
  { name: "PixNEO", icon: Repeat },
  { name: "Transações", icon: Repeat },
  { name: "Configurações", icon: Settings },
];

export default function Sidebar() {
  return (
    <aside className="w-20 md:w-56 bg-black border-r border-yellow-500/20 flex flex-col items-center md:items-start p-4 gap-6">
      {menu.map((item) => (
        <button
          key={item.name}
          className="flex items-center gap-3 hover:text-yellow-300 transition"
        >
          <item.icon />
          <span className="hidden md:block">{item.name}</span>
        </button>
      ))}
    </aside>
  );
}
import { useEffect, useState } from "react";

export default function BalanceCard() {
  const [balance, setBalance] = useState(12.345);

  useEffect(() => {
    const interval = setInterval(() => {
      setBalance((prev) => prev + Math.random() * 0.001);
    }, 3000);

    return () => clearInterval(interval);
  }, []);

  return (
    <div className="bg-yellow-500/10 border border-yellow-500/30 rounded-xl p-5">
      <p className="text-sm text-yellow-300">Saldo Total</p>
      <h2 className="text-3xl font-bold">{balance.toFixed(4)} NEX</h2>
      <p className="text-xs text-yellow-300 mt-1">≈ R$ 98.432,00 (estimado)</p>
    </div>
  );
}
export default function PixNeoCard() {
  return (
    <div className="bg-yellow-400 text-black rounded-xl p-5 flex flex-col gap-4 justify-between">
      <h2 className="text-lg font-bold">PixNEO</h2>

      <div className="flex gap-3">
        <button className="flex-1 bg-black text-yellow-400 py-2 rounded-lg hover:opacity-80">
          Enviar
        </button>
        <button className="flex-1 bg-black text-yellow-400 py-2 rounded-lg hover:opacity-80">
          Receber
        </button>
      </div>
    </div>
  );
}
const networks = [
  { name: "Stellar", balance: 1200 },
  { name: "Solana", balance: 8.23 },
  { name: "Polygon", balance: 450 },
];

export default function WalletCard() {
  return (
    <div className="bg-black border border-yellow-500/30 rounded-xl p-5">
      <h3 className="mb-3 font-semibold">Wallets</h3>

      <ul className="space-y-2">
        {networks.map((net) => (
          <li key={net.name} className="flex justify-between text-sm">
            <span>{net.name}</span>
            <span>{net.balance}</span>
          </li>
        ))}
      </ul>
    </div>
  );
}
const txs = [
  { id: 1, value: "+250 NEX", network: "Solana", status: "Concluída" },
  { id: 2, value: "-80 NEX", network: "Polygon", status: "Pendente" },
];

export default function TransactionsList() {
  return (
    <div className="bg-black border border-yellow-500/30 rounded-xl p-5">
      <h3 className="mb-4 font-semibold">Últimas Transações</h3>

      <ul className="space-y-3 text-sm">
        {txs.map((tx) => (
          <li key={tx.id} className="flex justify-between">
            <span>{tx.value}</span>
            <span>{tx.network}</span>
            <span
              className={
                tx.status === "Concluída"
                  ? "text-green-400"
                  : "text-yellow-400"
              }
            >
              {tx.status}
            </span>
          </li>
        ))}
      </ul>
    </div>
  );
}
const networks = [
  { name: "Stellar", latency: "32ms" },
  { name: "Solana", latency: "110ms" },
  { name: "Polygon", latency: "78ms" },
];

export default function NetworkStatus() {
  return (
    <div className="bg-black border border-yellow-500/30 rounded-xl p-5">
      <h3 className="mb-3 font-semibold">Status das Redes</h3>

      <ul className="space-y-2 text-sm">
        {networks.map((net) => (
          <li key={net.name} className="flex justify-between">
            <span>{net.name}</span>
            <span>{net.latency}</span>
          </li>
        ))}
      </ul>
    </div>
  );
}

            
           
