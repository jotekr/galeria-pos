import { useState, useEffect } from "react";
import { initializeApp } from "firebase/app";
import { getFirestore, collection, onSnapshot, addDoc, updateDoc, deleteDoc, doc, serverTimestamp } from "firebase/firestore";

const firebaseConfig = {
  apiKey: "AIzaSyCHaCwgsfIjyNLGNRYhca6G8CSuTlZ7RAg",
  authDomain: "galeria-pos-e9cd5.firebaseapp.com",
  databaseURL: "https://galeria-pos-e9cd5-default-rtdb.europe-west1.firebasedatabase.app",
  projectId: "galeria-pos-e9cd5",
  storageBucket: "galeria-pos-e9cd5.firebasestorage.app",
  messagingSenderId: "236668447421",
  appId: "1:236668447421:web:5b100bf2cb5ecd81bc65d4"
};

const app = initializeApp(firebaseConfig);
const db = getFirestore(app);

const fmt = (n) => Number(n).toFixed(2).replace(".", ",") + " zł";
const TAX_RATE = 0.23;
const CATEGORIES = ["Biżuteria", "Obrazy", "Rzeźby", "Pamiątki", "Inne"];
const CAT_COLORS = { "Biżuteria": "#d4a853", "Obrazy": "#7b9fd4", "Rzeźby": "#a07850", "Pamiątki": "#7db87d", "Inne": "#9090aa" };
const CAT_ICONS = { "Biżuteria": "💎", "Obrazy": "🖼️", "Rzeźby": "🗿", "Pamiątki": "🎁", "Inne": "📦" };

const DEMO_PRODUCTS = [
  { name: "Naszyjnik srebrny z bursztynem", price: 280, stock: 3, category: "Biżuteria", unit: "szt", artist: "Anna Kowalska", material: "Srebro 925, bursztyn bałtycki", desc: "Ręcznie robiony naszyjnik z naturalnym bursztynem" },
  { name: "Pierścionek z labradorytem", price: 350, stock: 1, category: "Biżuteria", unit: "szt", artist: "Marek Nowak", material: "Srebro 925, labradoryt", desc: "Autorski pierścionek z kamieniem księżycowym" },
  { name: "Obraz olejny – Gdański port", price: 1200, stock: 1, category: "Obrazy", unit: "szt", artist: "Jan Wiśniewski", material: "Olej na płótnie, 60x80cm", desc: "Pejzaż portowy, sygnowany przez artystę" },
  { name: "Ceramiczny kubek artystyczny", price: 95, stock: 8, category: "Pamiątki", unit: "szt", artist: "Studio Glina", material: "Ceramika, szkliwo", desc: "Ręcznie malowany kubek" },
  { name: "Figurka bursztynowa – ryba", price: 180, stock: 5, category: "Pamiątki", unit: "szt", artist: "Amber Art", material: "Bursztyn bałtycki", desc: "Rzeźbiony bursztyn, symbol Gdańska" },
  { name: "Kolczyki z muszlami", price: 120, stock: 6, category: "Biżuteria", unit: "szt", artist: "Anna Kowalska", material: "Srebro 925, muszle naturalne", desc: "Lekkie kolczyki na lato" },
];

function Modal({ children, onClose }) {
  return (
    <div style={{ position:"fixed", inset:0, background:"rgba(0,0,0,0.75)", display:"flex", alignItems:"center", justifyContent:"center", zIndex:1000, backdropFilter:"blur(6px)" }}>
      <div style={{ background:"#1c1a17", border:"1px solid #3a3528", borderRadius:16, padding:32, minWidth:480, maxWidth:600, maxHeight:"90vh", overflowY:"auto", position:"relative", boxShadow:"0 20px 60px rgba(0,0,0,0.5)" }}>
        <button onClick={onClose} style={{ position:"absolute", top:16, right:16, background:"none", border:"none", color:"#666", fontSize:20, cursor:"pointer" }}>✕</button>
        {children}
      </div>
    </div>
  );
}

function ReceiptModal({ tx, onClose }) {
  return (
    <Modal onClose={onClose}>
      <div style={{ fontFamily:"Georgia,serif", textAlign:"center" }}>
        <div style={{ fontSize:13, letterSpacing:4, color:"#c9a84c", textTransform:"uppercase", marginBottom:4 }}>Galeria & Sklep</div>
        <div style={{ fontSize:22, fontWeight:700, color:"#e8dcc8", marginBottom:4 }}>Potwierdzenie zakupu</div>
        <div style={{ color:"#666", fontSize:12, marginBottom:16 }}>Nr: #{tx.id} | {tx.date}</div>
        {tx.client && <div style={{ color:"#c9a84c", fontSize:13, marginBottom:12 }}>Klient: {tx.client}</div>}
        <hr style={{ border:"none", borderTop:"1px solid #3a3528", margin:"12px 0" }} />
        {tx.items.map((it, i) => (
          <div key={i} style={{ marginBottom:10, textAlign:"left", background:"#242018", borderRadius:8, padding:"10px 14px" }}>
            <div style={{ fontWeight:600, color:"#e8dcc8", fontSize:14 }}>{it.name}</div>
            {it.artist && <div style={{ fontSize:12, color:"#c9a84c", marginTop:2 }}>Autor: {it.artist}</div>}
            <div style={{ display:"flex", justifyContent:"space-between", marginTop:6 }}>
              <span style={{ color:"#888", fontSize:13 }}>x{it.qty}</span>
              <span style={{ color:"#c9a84c", fontWeight:700 }}>{fmt(it.price * it.qty)}</span>
            </div>
          </div>
        ))}
        <hr style={{ border:"none", borderTop:"1px solid #3a3528", margin:"12px 0" }} />
        <div style={{ display:"flex", justifyContent:"space-between", color:"#888", fontSize:13, marginBottom:4 }}><span>Netto:</span><span>{fmt(tx.total / (1+TAX_RATE))}</span></div>
        <div style={{ display:"flex", justifyContent:"space-between", color:"#888", fontSize:13, marginBottom:10 }}><span>VAT 23%:</span><span>{fmt(tx.total - tx.total/(1+TAX_RATE))}</span></div>
        <div style={{ display:"flex", justifyContent:"space-between", fontSize:20, fontWeight:700, color:"#c9a84c", marginBottom:16 }}><span>RAZEM</span><span>{fmt(tx.total)}</span></div>
        <div style={{ color:"#777", fontSize:13, marginBottom:16 }}>Płatność: {tx.payment}</div>
        <hr style={{ border:"none", borderTop:"1px solid #3a3528", margin:"12px 0" }} />
        <div style={{ color:"#555", fontSize:11, fontStyle:"italic" }}>Dziękujemy za zakup dzieła sztuki 🎨</div>
      </div>
    </Modal>
  );
}

export default function ArtPOS() {
  const [tab, setTab] = useState("kasa");
  const [products, setProducts] = useState([]);
  const [transactions, setTransactions] = useState([]);
  const [loading, setLoading] = useState(true);
  const [cart, setCart] = useState([]);
  const [search, setSearch] = useState("");
  const [catFilter, setCatFilter] = useState("Wszystkie");
  const [payment, setPayment] = useState("Karta");
  const [clientName, setClientName] = useState("");
  const [receipt, setReceipt] = useState(null);
  const [selectedProduct, setSelectedProduct] = useState(null);
  const [showForm, setShowForm] = useState(false);
  const [editProduct, setEditProduct] = useState(null);
  const [form, setForm] = useState({ name:"", price:"", stock:"1", category:"Biżuteria", unit:"szt", artist:"", material:"", desc:"" });
  const [successMsg, setSuccessMsg] = useState("");

  // Load products from Firestore
  useEffect(() => {
    const unsub = onSnapshot(collection(db, "products"), async (snap) => {
      if (snap.empty) {
        // First time – add demo products
        for (const p of DEMO_PRODUCTS) {
          await addDoc(collection(db, "products"), p);
        }
      } else {
        setProducts(snap.docs.map(d => ({ id: d.id, ...d.data() })));
        setLoading(false);
      }
    });
    return unsub;
  }, []);

  // Load transactions from Firestore
  useEffect(() => {
    const unsub = onSnapshot(collection(db, "transactions"), (snap) => {
      const txs = snap.docs.map(d => ({ id: d.id, ...d.data() }));
      txs.sort((a,b) => (b.createdAt?.seconds||0) - (a.createdAt?.seconds||0));
      setTransactions(txs);
    });
    return unsub;
  }, []);

  const categories = ["Wszystkie", ...CATEGORIES];
  const filtered = products.filter(p =>
    (catFilter === "Wszystkie" || p.category === catFilter) &&
    (p.name?.toLowerCase().includes(search.toLowerCase()) || p.artist?.toLowerCase().includes(search.toLowerCase()))
  );

  const cartTotal = cart.reduce((s, i) => s + i.price * i.qty, 0);

  const addToCart = (p) => {
    if (p.stock <= 0) return;
    setCart(prev => {
      const ex = prev.find(i => i.id === p.id);
      if (ex) return ex.qty >= p.stock ? prev : prev.map(i => i.id === p.id ? { ...i, qty: i.qty+1 } : i);
      return [...prev, { ...p, qty: 1 }];
    });
    setSelectedProduct(null);
  };

  const updateQty = (id, delta) => setCart(prev => prev.map(i => i.id===id ? { ...i, qty: Math.max(1,i.qty+delta) } : i).filter(i=>i.qty>0));
  const removeFromCart = (id) => setCart(prev => prev.filter(i => i.id!==id));

  const checkout = async () => {
    if (cart.length === 0) return;
    const now = new Date();
    const dateStr = now.toLocaleDateString("pl-PL") + " " + now.toLocaleTimeString("pl-PL", { hour:"2-digit", minute:"2-digit" });
    const newTx = {
      date: dateStr,
      items: cart.map(i => ({ name:i.name, qty:i.qty, price:i.price, artist:i.artist||"" })),
      total: cartTotal,
      payment,
      client: clientName,
      createdAt: serverTimestamp(),
    };
    const txRef = await addDoc(collection(db, "transactions"), newTx);
    // Update stock
    for (const item of cart) {
      const pRef = doc(db, "products", item.id);
      await updateDoc(pRef, { stock: item.stock - item.qty });
    }
    setCart([]);
    setClientName("");
    setReceipt({ ...newTx, id: txRef.id.slice(-6).toUpperCase() });
    showSuccess("✅ Sprzedaż zakończona!");
  };

  const showSuccess = (msg) => { setSuccessMsg(msg); setTimeout(() => setSuccessMsg(""), 3000); };

  const saveProduct = async () => {
    if (!form.name || !form.price) return;
    const data = { ...form, price: parseFloat(form.price), stock: parseInt(form.stock)||1 };
    if (editProduct) {
      await updateDoc(doc(db, "products", editProduct.id), data);
      showSuccess("✅ Produkt zaktualizowany!");
    } else {
      await addDoc(collection(db, "products"), data);
      showSuccess("✅ Produkt dodany!");
    }
    setShowForm(false); setEditProduct(null);
    setForm({ name:"", price:"", stock:"1", category:"Biżuteria", unit:"szt", artist:"", material:"", desc:"" });
  };

  const startEdit = (p) => {
    setEditProduct(p);
    setForm({ name:p.name, price:String(p.price), stock:String(p.stock), category:p.category, unit:p.unit||"szt", artist:p.artist||"", material:p.material||"", desc:p.desc||"" });
    setShowForm(true);
  };

  const deleteProduct = async (id) => { await deleteDoc(doc(db, "products", id)); showSuccess("🗑 Usunięto produkt"); };

  const totalRevenue = transactions.reduce((s,t) => s+t.total, 0);
  const topProducts = Object.entries(
    transactions.flatMap(t=>t.items||[]).reduce((acc,it) => { acc[it.name]=(acc[it.name]||0)+it.qty*it.price; return acc; },{})
  ).sort((a,b)=>b[1]-a[1]).slice(0,5);
  const byPayment = transactions.reduce((acc,t) => { acc[t.payment]=(acc[t.payment]||0)+t.total; return acc; },{});
  const lowStock = products.filter(p => p.stock<=1);

  const s = {
    app: { fontFamily:"'Segoe UI','Helvetica Neue',sans-serif", background:"#141210", minHeight:"100vh", color:"#e8dcc8", display:"flex", flexDirection:"column" },
    header: { background:"#1c1a17", borderBottom:"1px solid #3a3528", padding:"0 24px", display:"flex", alignItems:"center", gap:24, height:58, flexShrink:0 },
    logo: { color:"#c9a84c", fontWeight:700, fontSize:18, letterSpacing:1, fontFamily:"Georgia,serif", whiteSpace:"nowrap" },
    navBtn: (a) => ({ background:a?"#c9a84c":"transparent", color:a?"#141210":"#9a8a70", border:"none", borderRadius:8, padding:"6px 16px", fontWeight:600, fontSize:13, cursor:"pointer" }),
    body: { display:"flex", flex:1, height:"calc(100vh - 58px)", overflow:"hidden" },
    main: { flex:1, padding:22, overflowY:"auto" },
    sidebar: { width:320, background:"#1c1a17", borderLeft:"1px solid #3a3528", display:"flex", flexDirection:"column", padding:18, gap:10 },
    input: { background:"#242018", border:"1px solid #3a3528", borderRadius:8, padding:"10px 14px", color:"#e8dcc8", fontSize:14, width:"100%", boxSizing:"border-box", outline:"none" },
    label: { fontSize:12, color:"#9a8a70", marginBottom:4, display:"block", textTransform:"uppercase", letterSpacing:0.5 },
    table: { width:"100%", borderCollapse:"collapse", fontSize:13 },
    th: { textAlign:"left", padding:"10px 12px", color:"#9a8a70", fontWeight:600, fontSize:11, textTransform:"uppercase", letterSpacing:0.5, borderBottom:"1px solid #3a3528" },
    td: { padding:"10px 12px", borderBottom:"1px solid #2a2520", color:"#ccc0a8", verticalAlign:"middle" },
    actionBtn: { background:"#242018", border:"1px solid #3a3528", color:"#9a8a70", borderRadius:7, padding:"5px 12px", cursor:"pointer", fontSize:12, fontWeight:600 },
    statCard: { background:"#1c1a17", border:"1px solid #3a3528", borderRadius:12, padding:20 },
    goldBtn: { background:"#c9a84c", border:"none", color:"#141210", borderRadius:10, padding:"12px 20px", fontWeight:700, fontSize:14, cursor:"pointer", width:"100%" },
    payBtn: (a) => ({ flex:1, background:a?"#2a2518":"transparent", border:"1px solid "+(a?"#c9a84c":"#3a3528"), color:a?"#c9a84c":"#6a5a48", borderRadius:8, padding:"8px 0", cursor:"pointer", fontSize:13, fontWeight:a?700:400 }),
  };

  if (loading) return (
    <div style={{ ...s.app, alignItems:"center", justifyContent:"center" }}>
      <div style={{ color:"#c9a84c", fontSize:18, fontFamily:"Georgia,serif" }}>🎨 Ładowanie danych...</div>
    </div>
  );

  return (
    <div style={s.app}>
      <div style={s.header}>
        <div style={s.logo}>🎨 Galeria & Butik</div>
        <div style={{ display:"flex", gap:6 }}>
          {[["kasa","🛒 Kasa"],["magazyn","📦 Magazyn"],["transakcje","🧾 Transakcje"],["raporty","📊 Raporty"]].map(([k,l]) => (
            <button key={k} onClick={() => setTab(k)} style={s.navBtn(tab===k)}>{l}</button>
          ))}
        </div>
        {successMsg && <div style={{ marginLeft:"auto", background:"#2a3a28", color:"#7db87d", padding:"6px 16px", borderRadius:8, fontSize:13, fontWeight:600 }}>{successMsg}</div>}
      </div>

      {/* KASA */}
      {tab==="kasa" && (
        <div style={s.body}>
          <div style={s.main}>
            <div style={{ display:"flex", gap:10, marginBottom:16, flexWrap:"wrap", alignItems:"center" }}>
              <input value={search} onChange={e=>setSearch(e.target.value)} placeholder="🔍 Szukaj nazwy lub autora..." style={{ ...s.input, width:220 }} />
              {categories.map(c => (
                <button key={c} onClick={() => setCatFilter(c)} style={{ background:catFilter===c?(CAT_COLORS[c]||"#c9a84c")+"22":"transparent", color:catFilter===c?(CAT_COLORS[c]||"#c9a84c"):"#6a5a48", border:"1px solid "+(catFilter===c?(CAT_COLORS[c]||"#c9a84c"):"#3a3528"), borderRadius:8, padding:"5px 12px", fontSize:12, cursor:"pointer", fontWeight:catFilter===c?700:400 }}>
                  {CAT_ICONS[c]||""} {c}
                </button>
              ))}
            </div>
            <div style={{ display:"grid", gridTemplateColumns:"repeat(auto-fill,minmax(155px,1fr))", gap:12 }}>
              {filtered.map(p => (
                <div key={p.id} onClick={() => p.stock>0 && setSelectedProduct(p)}
                  style={{ background:"#1c1a17", border:"1px solid "+(p.stock===0?"#2a2520":"#3a3528"), borderRadius:12, padding:14, cursor:p.stock>0?"pointer":"default", opacity:p.stock===0?0.45:1, position:"relative" }}>
                  <div style={{ fontSize:10, color:CAT_COLORS[p.category]||"#9a8a70", fontWeight:700, textTransform:"uppercase", letterSpacing:0.5, marginBottom:6 }}>{CAT_ICONS[p.category]} {p.category}</div>
                  <div style={{ fontWeight:600, fontSize:13, color:"#e8dcc8", marginBottom:3, lineHeight:1.3 }}>{p.name}</div>
                  {p.artist && <div style={{ fontSize:11, color:"#9a8a70", marginBottom:6, fontStyle:"italic" }}>{p.artist}</div>}
                  <div style={{ color:"#c9a84c", fontWeight:700, fontSize:17, marginBottom:4 }}>{fmt(p.price)}</div>
                  {p.stock===1 && <div style={{ fontSize:11, color:"#e8a030", fontWeight:700 }}>⚡ Ostatnia sztuka!</div>}
                  {p.stock>1 && <div style={{ fontSize:11, color:"#6a5a48" }}>📦 {p.stock} szt</div>}
                  {p.stock===0 && <div style={{ position:"absolute", inset:0, background:"#14121088", borderRadius:12, display:"flex", alignItems:"center", justifyContent:"center", fontSize:12, color:"#ef6060", fontWeight:700 }}>BRAK</div>}
                </div>
              ))}
            </div>
          </div>

          <div style={s.sidebar}>
            <div style={{ fontWeight:700, fontSize:15, color:"#e8dcc8", fontFamily:"Georgia,serif" }}>🛒 Koszyk</div>
            <div style={{ flex:1, overflowY:"auto" }}>
              {cart.length===0 && <div style={{ color:"#4a3a28", fontSize:13, textAlign:"center", marginTop:50, fontStyle:"italic" }}>Wybierz produkt z lewej</div>}
              {cart.map(item => (
                <div key={item.id} style={{ padding:"10px 0", borderBottom:"1px solid #2a2520" }}>
                  <div style={{ display:"flex", justifyContent:"space-between", alignItems:"flex-start" }}>
                    <div style={{ flex:1, marginRight:8 }}>
                      <div style={{ fontSize:13, color:"#e8dcc8", fontWeight:600, lineHeight:1.3 }}>{item.name}</div>
                      {item.artist && <div style={{ fontSize:11, color:"#9a8a70", fontStyle:"italic" }}>{item.artist}</div>}
                      <div style={{ color:"#c9a84c", fontWeight:700, fontSize:14, marginTop:4 }}>{fmt(item.price*item.qty)}</div>
                    </div>
                    <button onClick={() => removeFromCart(item.id)} style={{ background:"none", border:"none", color:"#6a4040", cursor:"pointer", fontSize:16 }}>✕</button>
                  </div>
                  <div style={{ display:"flex", alignItems:"center", gap:8, marginTop:8 }}>
                    <button onClick={() => updateQty(item.id,-1)} style={{ background:"#242018", border:"1px solid #3a3528", color:"#ccc", width:26, height:26, borderRadius:6, cursor:"pointer" }}>−</button>
                    <span style={{ fontSize:14, fontWeight:600, minWidth:24, textAlign:"center" }}>{item.qty}</span>
                    <button onClick={() => updateQty(item.id,1)} style={{ background:"#242018", border:"1px solid #3a3528", color:"#ccc", width:26, height:26, borderRadius:6, cursor:"pointer" }}>+</button>
                  </div>
                </div>
              ))}
            </div>
            <div style={{ borderTop:"1px solid #3a3528", paddingTop:14 }}>
              <div style={{ marginBottom:10 }}>
                <label style={s.label}>Klient (opcjonalnie)</label>
                <input value={clientName} onChange={e=>setClientName(e.target.value)} placeholder="Imię i nazwisko" style={s.input} />
              </div>
              <div style={{ display:"flex", justifyContent:"space-between", fontSize:13, color:"#6a5a48", marginBottom:3 }}><span>Netto</span><span>{fmt(cartTotal/(1+TAX_RATE))}</span></div>
              <div style={{ display:"flex", justifyContent:"space-between", fontSize:13, color:"#6a5a48", marginBottom:10 }}><span>VAT 23%</span><span>{fmt(cartTotal-cartTotal/(1+TAX_RATE))}</span></div>
              <div style={{ display:"flex", justifyContent:"space-between", fontSize:22, fontWeight:700, color:"#c9a84c", marginBottom:14 }}><span>RAZEM</span><span>{fmt(cartTotal)}</span></div>
              <div style={{ display:"flex", gap:8, marginBottom:12 }}>
                {["Karta","Gotówka","BLIK"].map(m => <button key={m} onClick={() => setPayment(m)} style={s.payBtn(payment===m)}>{m}</button>)}
              </div>
              <button onClick={checkout} disabled={cart.length===0} style={{ ...s.goldBtn, opacity:cart.length===0?0.4:1 }}>✓ Sprzedaj i wystaw paragon</button>
            </div>
          </div>
        </div>
      )}

      {selectedProduct && (
        <Modal onClose={() => setSelectedProduct(null)}>
          <div style={{ fontSize:11, color:CAT_COLORS[selectedProduct.category], textTransform:"uppercase", letterSpacing:1, fontWeight:700, marginBottom:8 }}>{CAT_ICONS[selectedProduct.category]} {selectedProduct.category}</div>
          <div style={{ fontSize:22, fontWeight:700, color:"#e8dcc8", fontFamily:"Georgia,serif", marginBottom:4 }}>{selectedProduct.name}</div>
          {selectedProduct.artist && <div style={{ color:"#c9a84c", fontSize:14, marginBottom:12, fontStyle:"italic" }}>Autor: {selectedProduct.artist}</div>}
          {selectedProduct.material && <div style={{ color:"#9a8a70", fontSize:13, marginBottom:6 }}>📐 {selectedProduct.material}</div>}
          {selectedProduct.desc && <div style={{ color:"#ccc0a8", fontSize:14, marginBottom:16, lineHeight:1.6 }}>{selectedProduct.desc}</div>}
          <div style={{ display:"flex", justifyContent:"space-between", alignItems:"center", marginBottom:20 }}>
            <div style={{ fontSize:28, fontWeight:800, color:"#c9a84c" }}>{fmt(selectedProduct.price)}</div>
            {selectedProduct.stock===1 && <div style={{ background:"#e8a03022", color:"#e8a030", padding:"4px 12px", borderRadius:8, fontSize:13, fontWeight:700 }}>⚡ Ostatnia sztuka!</div>}
            {selectedProduct.stock>1 && <div style={{ color:"#6a5a48", fontSize:13 }}>📦 {selectedProduct.stock} w magazynie</div>}
          </div>
          <button onClick={() => addToCart(selectedProduct)} style={s.goldBtn}>🛒 Dodaj do koszyka</button>
        </Modal>
      )}

      {/* MAGAZYN */}
      {tab==="magazyn" && (
        <div style={s.main}>
          <div style={{ display:"flex", justifyContent:"space-between", alignItems:"center", marginBottom:20 }}>
            <div style={{ fontWeight:700, fontSize:18, fontFamily:"Georgia,serif" }}>📦 Magazyn produktów</div>
            <button onClick={() => { setShowForm(true); setEditProduct(null); setForm({ name:"", price:"", stock:"1", category:"Biżuteria", unit:"szt", artist:"", material:"", desc:"" }); }} style={{ ...s.goldBtn, width:"auto" }}>+ Dodaj produkt</button>
          </div>
          {lowStock.length>0 && (
            <div style={{ background:"#2a1e1022", border:"1px solid #c9843033", borderRadius:10, padding:"12px 16px", marginBottom:16, display:"flex", gap:12, alignItems:"center" }}>
              <span>⚠️</span>
              <div>
                <div style={{ color:"#e8a030", fontWeight:700, fontSize:13 }}>Niski stan magazynowy</div>
                <div style={{ color:"#9a8a70", fontSize:12 }}>{lowStock.map(p=>p.name).join(", ")}</div>
              </div>
            </div>
          )}
          <table style={s.table}>
            <thead><tr>{["Produkt","Autor","Kategoria","Cena","Stan",""].map(h=><th key={h} style={s.th}>{h}</th>)}</tr></thead>
            <tbody>
              {products.map(p => (
                <tr key={p.id}>
                  <td style={s.td}><b style={{ color:"#e8dcc8" }}>{p.name}</b>{p.material&&<div style={{ fontSize:11, color:"#6a5a48", marginTop:2 }}>{p.material}</div>}</td>
                  <td style={{ ...s.td, fontStyle:"italic", color:"#c9a84c", fontSize:12 }}>{p.artist||"—"}</td>
                  <td style={s.td}><span style={{ background:(CAT_COLORS[p.category]||"#9090aa")+"22", color:CAT_COLORS[p.category]||"#9090aa", borderRadius:6, padding:"2px 8px", fontSize:12, fontWeight:600 }}>{CAT_ICONS[p.category]} {p.category}</span></td>
                  <td style={{ ...s.td, color:"#c9a84c", fontWeight:700 }}>{fmt(p.price)}</td>
                  <td style={s.td}><span style={{ background:p.stock===0?"#ef606022":p.stock===1?"#e8a03022":"#7db87d22", color:p.stock===0?"#ef6060":p.stock===1?"#e8a030":"#7db87d", borderRadius:6, padding:"2px 8px", fontSize:12, fontWeight:700 }}>{p.stock===0?"BRAK":p.stock===1?"Ostatnia!":p.stock+" szt"}</span></td>
                  <td style={s.td}>
                    <button onClick={() => startEdit(p)} style={{ ...s.actionBtn, marginRight:6 }}>✏️</button>
                    <button onClick={() => deleteProduct(p.id)} style={{ ...s.actionBtn, color:"#ef6060" }}>🗑</button>
                  </td>
                </tr>
              ))}
            </tbody>
          </table>
          {showForm && (
            <Modal onClose={() => { setShowForm(false); setEditProduct(null); }}>
              <div style={{ fontWeight:700, fontSize:18, marginBottom:20, color:"#c9a84c", fontFamily:"Georgia,serif" }}>{editProduct?"✏️ Edytuj produkt":"➕ Nowy produkt"}</div>
              <div style={{ display:"grid", gridTemplateColumns:"1fr 1fr", gap:14 }}>
                <div style={{ gridColumn:"1/-1" }}><label style={s.label}>Nazwa produktu *</label><input value={form.name} onChange={e=>setForm(f=>({...f,name:e.target.value}))} style={s.input} /></div>
                <div><label style={s.label}>Cena (zł) *</label><input type="number" value={form.price} onChange={e=>setForm(f=>({...f,price:e.target.value}))} style={s.input} /></div>
                <div><label style={s.label}>Stan magazynowy</label><input type="number" value={form.stock} onChange={e=>setForm(f=>({...f,stock:e.target.value}))} style={s.input} min="0" /></div>
                <div><label style={s.label}>Kategoria</label><select value={form.category} onChange={e=>setForm(f=>({...f,category:e.target.value}))} style={s.input}>{CATEGORIES.map(c=><option key={c}>{c}</option>)}</select></div>
                <div><label style={s.label}>Autor / Artysta</label><input value={form.artist} onChange={e=>setForm(f=>({...f,artist:e.target.value}))} style={s.input} /></div>
                <div style={{ gridColumn:"1/-1" }}><label style={s.label}>Materiał / Technika</label><input value={form.material} onChange={e=>setForm(f=>({...f,material:e.target.value}))} style={s.input} /></div>
                <div style={{ gridColumn:"1/-1" }}><label style={s.label}>Opis</label><input value={form.desc} onChange={e=>setForm(f=>({...f,desc:e.target.value}))} style={s.input} /></div>
              </div>
              <button onClick={saveProduct} style={{ ...s.goldBtn, marginTop:20 }}>{editProduct?"💾 Zapisz zmiany":"✅ Dodaj produkt"}</button>
            </Modal>
          )}
        </div>
      )}

      {/* TRANSAKCJE */}
      {tab==="transakcje" && (
        <div style={s.main}>
          <div style={{ fontWeight:700, fontSize:18, fontFamily:"Georgia,serif", marginBottom:20 }}>🧾 Historia transakcji</div>
          <table style={s.table}>
            <thead><tr>{["Nr","Data","Produkty","Klient","Kwota","Płatność",""].map(h=><th key={h} style={s.th}>{h}</th>)}</tr></thead>
            <tbody>
              {transactions.map(tx => (
                <tr key={tx.id}>
                  <td style={s.td}><b>#{(tx.id||"").slice(-6).toUpperCase()}</b></td>
                  <td style={{ ...s.td, fontSize:12 }}>{tx.date}</td>
                  <td style={{ ...s.td, fontSize:12 }}>{(tx.items||[]).map(i=>i.name).join(", ")}</td>
                  <td style={{ ...s.td, fontSize:12, fontStyle:"italic", color:"#c9a84c" }}>{tx.client||"—"}</td>
                  <td style={{ ...s.td, color:"#c9a84c", fontWeight:700 }}>{fmt(tx.total)}</td>
                  <td style={s.td}><span style={{ background:tx.payment==="Karta"?"#6b9fd422":tx.payment==="BLIK"?"#a07fd422":"#7db87d22", color:tx.payment==="Karta"?"#6b9fd4":tx.payment==="BLIK"?"#a07fd4":"#7db87d", borderRadius:6, padding:"2px 8px", fontSize:12, fontWeight:600 }}>{tx.payment}</span></td>
                  <td style={s.td}><button onClick={() => setReceipt({ ...tx, id:(tx.id||"").slice(-6).toUpperCase() })} style={s.actionBtn}>🧾 Paragon</button></td>
                </tr>
              ))}
            </tbody>
          </table>
        </div>
      )}

      {/* RAPORTY */}
      {tab==="raporty" && (
        <div style={s.main}>
          <div style={{ fontWeight:700, fontSize:18, fontFamily:"Georgia,serif", marginBottom:20 }}>📊 Raporty sprzedaży</div>
          <div style={{ display:"grid", gridTemplateColumns:"repeat(3,1fr)", gap:16, marginBottom:24 }}>
            {[["Przychód łączny",fmt(totalRevenue),"💰"],["Liczba transakcji",transactions.length,"🧾"],["Śr. wartość zakupu",fmt(totalRevenue/(transactions.length||1)),"📈"]].map(([l,v,i]) => (
              <div key={l} style={s.statCard}>
                <div style={{ fontSize:22, marginBottom:8 }}>{i}</div>
                <div style={{ fontSize:26, fontWeight:800, color:"#c9a84c" }}>{v}</div>
                <div style={{ fontSize:12, color:"#6a5a48", marginTop:4, textTransform:"uppercase", letterSpacing:0.5 }}>{l}</div>
              </div>
            ))}
          </div>
          <div style={{ display:"grid", gridTemplateColumns:"1fr 1fr", gap:16 }}>
            <div style={s.statCard}>
              <div style={{ fontWeight:700, marginBottom:14, color:"#e8dcc8", fontFamily:"Georgia,serif" }}>🏆 Najlepiej sprzedające się</div>
              {topProducts.length===0 && <div style={{ color:"#4a3a28", fontSize:13 }}>Brak transakcji</div>}
              {topProducts.map(([name,rev],i) => (
                <div key={name} style={{ display:"flex", justifyContent:"space-between", padding:"8px 0", borderBottom:"1px solid #2a2520" }}>
                  <div style={{ display:"flex", gap:10, alignItems:"center" }}>
                    <span style={{ color:"#c9a84c", fontWeight:700, fontSize:13 }}>#{i+1}</span>
                    <span style={{ fontSize:13, color:"#ccc0a8" }}>{name}</span>
                  </div>
                  <span style={{ color:"#c9a84c", fontWeight:700 }}>{fmt(rev)}</span>
                </div>
              ))}
            </div>
            <div style={s.statCard}>
              <div style={{ fontWeight:700, marginBottom:14, color:"#e8dcc8", fontFamily:"Georgia,serif" }}>💳 Metody płatności</div>
              {Object.entries(byPayment).map(([method,amount]) => {
                const pct = Math.round((amount/totalRevenue)*100)||0;
                return (
                  <div key={method} style={{ marginBottom:12 }}>
                    <div style={{ display:"flex", justifyContent:"space-between", marginBottom:5, fontSize:13 }}>
                      <span style={{ color:"#ccc0a8" }}>{method}</span>
                      <span style={{ color:"#c9a84c", fontWeight:700 }}>{fmt(amount)} ({pct}%)</span>
                    </div>
                    <div style={{ background:"#242018", borderRadius:99, height:6 }}>
                      <div style={{ background:"#c9a84c", borderRadius:99, height:6, width:`${pct}%` }} />
                    </div>
                  </div>
                );
              })}
              <div style={{ marginTop:16, padding:12, background:"#242018", borderRadius:10 }}>
                <div style={{ fontSize:11, color:"#6a5a48", marginBottom:4, textTransform:"uppercase", letterSpacing:0.5 }}>VAT do odprowadzenia</div>
                <div style={{ fontSize:22, fontWeight:800, color:"#ef6060" }}>{fmt(totalRevenue-totalRevenue/(1+TAX_RATE))}</div>
              </div>
            </div>
          </div>
        </div>
      )}

      {receipt && <ReceiptModal tx={receipt} onClose={() => setReceipt(null)} />}
    </div>
  );
}
