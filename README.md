# -import { useState, useEffect, useRef } from "react";

// ── SVG Icons ──────────────────────────────────────────────────
const Icon = ({ name, size = 20, color = "currentColor" }) => {
  const paths = {
    home:     <path strokeLinecap="round" strokeLinejoin="round" d="M2.25 12l8.954-8.955c.44-.439 1.152-.439 1.591 0L21.75 12M4.5 9.75v10.125c0 .621.504 1.125 1.125 1.125H9.75v-4.875c0-.621.504-1.125 1.125-1.125h2.25c.621 0 1.125.504 1.125 1.125V21h4.125c.621 0 1.125-.504 1.125-1.125V9.75"/>,
    check:    <path strokeLinecap="round" strokeLinejoin="round" d="M9 12.75L11.25 15 15 9.75M21 12a9 9 0 11-18 0 9 9 0 0118 0z"/>,
    target:   <><circle cx="12" cy="12" r="9" fill="none"/><circle cx="12" cy="12" r="5" fill="none"/><circle cx="12" cy="12" r="1.5" fill={color}/></>,
    calendar: <path strokeLinecap="round" strokeLinejoin="round" d="M6.75 3v2.25M17.25 3v2.25M3 18.75V7.5a2.25 2.25 0 012.25-2.25h13.5A2.25 2.25 0 0121 7.5v11.25m-18 0A2.25 2.25 0 005.25 21h13.5A2.25 2.25 0 0021 18.75m-18 0v-7.5A2.25 2.25 0 015.25 9h13.5A2.25 2.25 0 0121 11.25v7.5m-9-6h.008v.008H12v-.008zM12 15h.008v.008H12V15zm0 2.25h.008v.008H12v-.008zM9.75 15h.008v.008H9.75V15zm0 2.25h.008v.008H9.75v-.008zM7.5 15h.008v.008H7.5V15zm0 2.25h.008v.008H7.5v-.008zm6.75-4.5h.008v.008h-.008v-.008zm0 2.25h.008v.008h-.008V15zm0 2.25h.008v.008h-.008v-.008zm2.25-4.5h.008v.008H16.5v-.008zm0 2.25h.008v.008H16.5V15z"/>,
    ai:       <path strokeLinecap="round" strokeLinejoin="round" d="M9.813 15.904L9 18.75l-.813-2.846a4.5 4.5 0 00-3.09-3.09L2.25 12l2.846-.813a4.5 4.5 0 003.09-3.09L9 5.25l.813 2.846a4.5 4.5 0 003.09 3.09L15.75 12l-2.846.813a4.5 4.5 0 00-3.09 3.09z"/>,
    send:     <path strokeLinecap="round" strokeLinejoin="round" d="M6 12L3.269 3.126A59.768 59.768 0 0121.485 12 59.77 59.77 0 013.27 20.876L5.999 12zm0 0h7.5"/>,
    close:    <path strokeLinecap="round" strokeLinejoin="round" d="M6 18L18 6M6 6l12 12"/>,
    chevL:    <path strokeLinecap="round" strokeLinejoin="round" d="M15.75 19.5L8.25 12l7.5-7.5"/>,
    chevR:    <path strokeLinecap="round" strokeLinejoin="round" d="M8.25 4.5l7.5 7.5-7.5 7.5"/>,
    bell:     <path strokeLinecap="round" strokeLinejoin="round" d="M14.857 17.082a23.848 23.848 0 005.454-1.31A8.967 8.967 0 0118 9.75v-.7V9A6 6 0 006 9v.75a8.967 8.967 0 01-2.312 6.022c1.733.64 3.56 1.085 5.455 1.31m5.714 0a24.255 24.255 0 01-5.714 0m5.714 0a3 3 0 11-5.714 0"/>,
    work:     <path strokeLinecap="round" strokeLinejoin="round" d="M20.25 14.15v4.25c0 1.094-.787 2.036-1.872 2.18-2.087.277-4.216.42-6.378.42s-4.291-.143-6.378-.42c-1.085-.144-1.872-1.086-1.872-2.18v-4.25m16.5 0a2.18 2.18 0 00.75-1.661V8.706c0-1.081-.768-2.015-1.837-2.175a48.114 48.114 0 00-3.413-.387m4.5 8.006c-.194.165-.42.295-.673.38A23.978 23.978 0 0112 15.75c-2.648 0-5.195-.429-7.577-1.22a2.016 2.016 0 01-.673-.38m0 0A2.18 2.18 0 013 12.489V8.706c0-1.081.768-2.015 1.837-2.175a48.111 48.111 0 013.413-.387m7.5 0V5.25A2.25 2.25 0 0013.5 3h-3a2.25 2.25 0 00-2.25 2.25v.894m7.5 0a48.667 48.667 0 00-7.5 0"/>,
    plus:     <path strokeLinecap="round" strokeLinejoin="round" d="M12 4.5v15m7.5-7.5h-15"/>,
    trash:    <path strokeLinecap="round" strokeLinejoin="round" d="M14.74 9l-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 01-2.244 2.077H8.084a2.25 2.25 0 01-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 00-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 013.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 00-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 00-7.5 0"/>,
  };
  const isTarget = name === "target";
  return (
    <svg width={size} height={size} viewBox="0 0 24 24" fill="none" stroke={color} strokeWidth={1.8}>
      {paths[name]}
    </svg>
  );
};

// ── Palette ───────────────────────────────────────────────────
const P = {
  bg:       "#fff5f7",
  card:     "#ffffff",
  border:   "#fce7f3",
  pink:     "#f472b6",
  pinkDark: "#db2777",
  pinkLight:"#fdf2f8",
  pinkMid:  "#fbcfe8",
  work:     { main:"#f472b6", light:"#fdf2f8", border:"#fbcfe8", text:"#9d174d" },
  personal: { main:"#c084fc", light:"#faf5ff", border:"#e9d5ff", text:"#6b21a8" },
  exam:     { main:"#fb7185", light:"#fff1f2", border:"#fecdd3", text:"#9f1239" },
  green:    "#10b981",
  orange:   "#f59e0b",
  text:     "#1e1b4b",
  sub:      "#9ca3af",
};

// ── Utilities ─────────────────────────────────────────────────
const parseDate = (str) => {
  // supports "2026-07-10", "7/10", "07/10", "7월10일", "7월 10일"
  const now = new Date();
  const year = now.getFullYear();
  let m, d;
  let match = str.match(/(\d{4})[.\-\/](\d{1,2})[.\-\/](\d{1,2})/);
  if (match) return new Date(+match[1], +match[2]-1, +match[3]);
  match = str.match(/(\d{1,2})[\/](\d{1,2})/);
  if (match) return new Date(year, +match[1]-1, +match[2]);
  match = str.match(/(\d{1,2})월\s*(\d{1,2})일/);
  if (match) return new Date(year, +match[1]-1, +match[2]);
  return null;
};

const fmtDate = (d) => `${d.getMonth()+1}/${d.getDate()}`;
const fmtFull = (d) => `${d.getFullYear()}.${String(d.getMonth()+1).padStart(2,"0")}.${String(d.getDate()).padStart(2,"0")}`;
const daysBetween = (a, b) => Math.round((b-a)/(1000*60*60*24));
const sameDay = (a, b) => a.getFullYear()===b.getFullYear() && a.getMonth()===b.getMonth() && a.getDate()===b.getDate();

// ── Initial Data ──────────────────────────────────────────────
const INIT_EVENTS = [
  { id:1, type:"work",     title:"보험 교육 미팅",       date:"2026-06-26", time:"09:00" },
  { id:2, type:"personal", title:"수영",                 date:"2026-06-26", time:"18:00" },
  { id:3, type:"work",     title:"SQLD 스터디",          date:"2026-06-26", time:"20:00" },
  { id:4, type:"work",     title:"보험계약관리역 접수",   date:"2026-06-27", time:"종일", badge:"접수" },
  { id:5, type:"work",     title:"SQLD 시험",            date:"2026-07-10", time:"종일", badge:"시험", isExam:true, regDate:"2026.06.05~06.15" },
  { id:6, type:"work",     title:"보험계약관리역 시험",   date:"2026-07-27", time:"종일", badge:"시험", isExam:true, regDate:"2026.06.27~07.07" },
  { id:7, type:"work",     title:"AFPK 1차 시험",        date:"2026-09-14", time:"종일", badge:"시험", isExam:true, regDate:"2026.07.20~08.01" },
  { id:8, type:"personal", title:"영어회화 IM3 테스트",  date:"2026-06-30", time:"종일", badge:"시험", isExam:true, regDate:"2026.06.01~06.20" },
  { id:9, type:"personal", title:"풀마라톤 대회",         date:"2026-11-03", time:"종일", badge:"대회" },
  { id:10, type:"personal",title:"제주 여행",             date:"2026-08-10", time:"종일" },
];

const TODOS = {
  daily: [
    { id:1, text:"SQLD 문제 30개", done:false, type:"work" },
    { id:2, text:"수영 1시간",      done:false, type:"personal" },
    { id:3, text:"영어 단어 20개", done:false, type:"personal" },
    { id:4, text:"보험 자료 검토",  done:false, type:"work" },
  ],
  weekly: [
    { id:5, text:"보험계약관리역 모의고사",  done:false, type:"work" },
    { id:6, text:"러닝 3회",                done:true,  type:"personal" },
    { id:7, text:"유튜브 기획안 작성",      done:false, type:"work" },
    { id:8, text:"방 청소",                 done:false, type:"personal" },
  ],
  monthly: [
    { id:9,  text:"SQLD 파트별 총정리",        done:false, type:"work" },
    { id:10, text:"보험교육 자료 제출",        done:false, type:"work" },
    { id:11, text:"영어 IM3 모의 시험",        done:false, type:"personal" },
    { id:12, text:"마라톤 장거리 훈련 (20km)", done:false, type:"personal" },
  ],
};

const GOALS = [
  { id:1, label:"SQLD 자격증",  progress:68, target:"2026.07", type:"work",     color:P.work.main },
  { id:2, label:"AFPK 취득",    progress:32, target:"2026.09", type:"work",     color:"#f9a8d4" },
  { id:3, label:"영어 IM3",     progress:51, target:"2026.06", type:"personal", color:P.personal.main },
  { id:4, label:"풀마라톤 완주", progress:44, target:"2026.11", type:"personal", color:"#a78bfa" },
  { id:5, label:"유튜브 시작",   progress:15, target:"2026.08", type:"personal", color:"#fb923c" },
];

let nextId = 100;

// ── AI Chat (with calendar injection) ─────────────────────────
function AIChat({ onClose, onAddEvent }) {
  const [msgs, setMsgs] = useState([{ role:"ai", text:"안녕하세요! 📅 날짜와 일정을 말씀해 주시면 캘린더에 바로 추가해드려요.\n\n예) '7월 15일 치과 예약 개인' 또는 '2026-08-01 팀 회의 업무'" }]);
  const [input, setInput] = useState("");
  const [loading, setLoading] = useState(false);
  const bottomRef = useRef(null);

  useEffect(() => { bottomRef.current?.scrollIntoView({ behavior:"smooth" }); }, [msgs]);

  async function send() {
    if (!input.trim() || loading) return;
    const txt = input.trim(); setInput("");
    setMsgs(m => [...m, { role:"user", text:txt }]); setLoading(true);

    try {
      const res = await fetch("https://api.anthropic.com/v1/messages", {
        method:"POST", headers:{"Content-Type":"application/json"},
        body: JSON.stringify({
          model:"claude-sonnet-4-6", max_tokens:800,
          system:`당신은 Life Manager OS의 AI 비서입니다. 파스텔 핑크 테마의 일정 관리 앱입니다.

사용자가 날짜와 일정을 말하면, 반드시 아래 JSON 형식을 응답에 포함하세요:
[CALENDAR_ADD]{"title":"일정명","date":"YYYY-MM-DD","type":"work 또는 personal","time":"HH:MM 또는 종일","badge":"시험|접수|대회 중 해당하면 넣고 없으면 null"}[/CALENDAR_ADD]

type 판단: 업무/공부/시험/자격증/회의 → work, 운동/여행/개인/가족/취미 → personal

JSON 블록 외에 친근한 한국어로 짧게 응답하세요. 이모지 활용.
일정 추가가 아닌 일반 질문은 JSON 없이 답하세요.
현재상태: SQLD D-14, 보험관리역 D-28, 목표: SQLD 68% / AFPK 32% / 영어 51%`,
          messages: msgs.slice(1).map(m=>({ role:m.role==="ai"?"assistant":"user", content:m.text })).concat([{role:"user",content:txt}])
        })
      });
      const data = await res.json();
      const reply = data.content?.map(c=>c.text||"").join("") || "다시 시도해주세요.";

      // extract calendar events
      const regex = /\[CALENDAR_ADD\]([\s\S]*?)\[\/CALENDAR_ADD\]/g;
      let match; const added = [];
      let cleaned = reply;
      while ((match = regex.exec(reply)) !== null) {
        try {
          const ev = JSON.parse(match[1]);
          if (ev.title && ev.date) {
            onAddEvent({ id: nextId++, ...ev, badge: ev.badge || undefined });
            added.push(ev.title);
          }
        } catch {}
        cleaned = cleaned.replace(match[0], "");
      }
      cleaned = cleaned.trim();
      if (added.length) cleaned += `\n\n✅ 캘린더에 추가됨: ${added.join(", ")}`;
      setMsgs(m => [...m, { role:"ai", text: cleaned }]);
    } catch {
      setMsgs(m => [...m, { role:"ai", text:"연결 오류가 발생했어요. 다시 시도해주세요." }]);
    }
    setLoading(false);
  }

  return (
    <div style={{ position:"fixed", inset:0, background:"rgba(30,10,30,0.35)", zIndex:1000, display:"flex", alignItems:"flex-end", justifyContent:"center" }} onClick={onClose}>
      <div style={{ width:"100%", maxWidth:480, height:"80vh", background:"#fff", borderRadius:"24px 24px 0 0", display:"flex", flexDirection:"column", boxShadow:"0 -12px 48px rgba(244,114,182,0.15)" }} onClick={e=>e.stopPropagation()}>
        <div style={{ padding:"18px 20px 14px", borderBottom:`1px solid ${P.border}`, display:"flex", alignItems:"center", gap:12 }}>
          <div style={{ width:40, height:40, borderRadius:"50%", background:`linear-gradient(135deg,${P.pink},${P.personal.main})`, display:"flex", alignItems:"center", justifyContent:"center" }}>
            <Icon name="ai" size={18} color="#fff" />
          </div>
          <div style={{ flex:1 }}>
            <div style={{ fontWeight:700, fontSize:14, color:P.text }}>AI 비서</div>
            <div style={{ fontSize:11, color:P.green, fontWeight:600 }}>● 일정 자동 등록 가능</div>
          </div>
          <button onClick={onClose} style={{ background:P.pinkLight, border:`1px solid ${P.border}`, borderRadius:10, width:34, height:34, display:"flex", alignItems:"center", justifyContent:"center", cursor:"pointer" }}>
            <Icon name="close" size={16} color={P.pinkDark} />
          </button>
        </div>

        <div style={{ flex:1, overflowY:"auto", padding:"14px 18px", display:"flex", flexDirection:"column", gap:10 }}>
          {msgs.map((m,i) => (
            <div key={i} style={{ display:"flex", justifyContent:m.role==="user"?"flex-end":"flex-start" }}>
              {m.role==="ai" && <div style={{ width:28, height:28, borderRadius:"50%", background:`linear-gradient(135deg,${P.pink},${P.personal.main})`, display:"flex", alignItems:"center", justifyContent:"center", flexShrink:0, marginRight:8, marginTop:2 }}><Icon name="ai" size={13} color="#fff"/></div>}
              <div style={{ maxWidth:"76%", padding:"11px 15px", borderRadius:m.role==="user"?"18px 18px 4px 18px":"18px 18px 18px 4px", background:m.role==="user"?`linear-gradient(135deg,${P.pink},${P.personal.main})`:"#fdf2f8", color:m.role==="user"?"#fff":P.text, fontSize:13.5, lineHeight:1.7, border:m.role==="user"?"none":`1px solid ${P.border}`, whiteSpace:"pre-wrap" }}>{m.text}</div>
            </div>
          ))}
          {loading && <div style={{ display:"flex", alignItems:"center", gap:8 }}><div style={{ width:28, height:28, borderRadius:"50%", background:`linear-gradient(135deg,${P.pink},${P.personal.main})`, display:"flex", alignItems:"center", justifyContent:"center" }}><Icon name="ai" size={13} color="#fff"/></div><div style={{ padding:"11px 16px", borderRadius:"18px 18px 18px 4px", background:"#fdf2f8", border:`1px solid ${P.border}`, fontSize:18, color:P.pink }}>···</div></div>}
          <div ref={bottomRef}/>
        </div>

        <div style={{ padding:"12px 16px 28px", borderTop:`1px solid ${P.border}`, display:"flex", gap:8 }}>
          <input value={input} onChange={e=>setInput(e.target.value)} onKeyDown={e=>e.key==="Enter"&&send()}
            placeholder="예) 7월 20일 치과 예약 개인"
            style={{ flex:1, background:P.pinkLight, border:`1.5px solid ${P.pinkMid}`, borderRadius:14, padding:"12px 16px", fontSize:14, color:P.text, outline:"none" }}/>
          <button onClick={send} disabled={loading} style={{ width:46, height:46, borderRadius:14, flexShrink:0, background:loading?"#e2e8f0":`linear-gradient(135deg,${P.pink},${P.personal.main})`, border:"none", cursor:loading?"default":"pointer", display:"flex", alignItems:"center", justifyContent:"center" }}>
            <Icon name="send" size={18} color="#fff"/>
          </button>
        </div>
      </div>
    </div>
  );
}

// ── Calendar Grid ─────────────────────────────────────────────
function CalendarGrid({ year, month, events, onSelectDay, selectedDay }) {
  const firstDay = new Date(year, month, 1).getDay();
  const daysInMonth = new Date(year, month+1, 0).getDate();
  const today = new Date();
  const cells = [];
  for (let i=0; i<firstDay; i++) cells.push(null);
  for (let d=1; d<=daysInMonth; d++) cells.push(d);

  const dayEvs = (d) => {
    if (!d) return [];
    const dt = new Date(year, month, d);
    return events.filter(e => sameDay(new Date(e.date), dt));
  };

  const weeks = [];
  for (let i=0; i<cells.length; i+=7) weeks.push(cells.slice(i,i+7));

  return (
    <div>
      {/* Day headers */}
      <div style={{ display:"grid", gridTemplateColumns:"repeat(7,1fr)", marginBottom:4 }}>
        {["일","월","화","수","목","금","토"].map((d,i)=>(
          <div key={d} style={{ textAlign:"center", fontSize:11, fontWeight:700, color:i===0?"#f43f5e":i===6?"#6366f1":P.sub, padding:"6px 0" }}>{d}</div>
        ))}
      </div>
      {/* Weeks */}
      {weeks.map((week,wi)=>(
        <div key={wi} style={{ display:"grid", gridTemplateColumns:"repeat(7,1fr)", borderTop:`1px solid ${P.border}` }}>
          {week.map((d,di)=>{
            const evs = dayEvs(d);
            const dt = d ? new Date(year, month, d) : null;
            const isToday = dt && sameDay(dt, today);
            const isSel = dt && selectedDay && sameDay(dt, selectedDay);
            const dow = (di) % 7;
            const isSun = dow===0, isSat = dow===6;
            return (
              <div key={di} onClick={()=>d && onSelectDay(new Date(year,month,d))}
                style={{ minHeight:52, padding:"4px 3px", cursor:d?"pointer":"default", background:isSel?"#fdf2f8":isToday?`${P.pinkLight}`:"transparent", borderRadius:d?8:0, position:"relative" }}>
                {d && (
                  <>
                    <div style={{ width:22, height:22, borderRadius:"50%", background:isToday?P.pink:"transparent", display:"flex", alignItems:"center", justifyContent:"center", margin:"0 auto 2px" }}>
                      <span style={{ fontSize:12, fontWeight:isToday?800:500, color:isToday?"#fff":isSun?"#f43f5e":isSat?"#818cf8":P.text }}>{d}</span>
                    </div>
                    <div style={{ display:"flex", flexDirection:"column", gap:2 }}>
                      {evs.slice(0,2).map((e,i)=>(
                        <div key={i} style={{ fontSize:9, fontWeight:700, borderRadius:4, padding:"1px 3px", background:e.type==="work"?P.work.light:P.personal.light, color:e.type==="work"?P.work.text:P.personal.text, overflow:"hidden", whiteSpace:"nowrap", textOverflow:"ellipsis", border:`1px solid ${e.type==="work"?P.work.border:P.personal.border}` }}>
                          {e.title}
                        </div>
                      ))}
                      {evs.length>2 && <div style={{ fontSize:9, color:P.sub, fontWeight:600, textAlign:"center" }}>+{evs.length-2}</div>}
                    </div>
                  </>
                )}
              </div>
            );
          })}
        </div>
      ))}
    </div>
  );
}

// ── Main App ──────────────────────────────────────────────────
export default function App() {
  const [tab, setTab] = useState("dashboard");
  const [todos, setTodos] = useState(TODOS);
  const [todoFilter, setTodoFilter] = useState("daily");
  const [events, setEvents] = useState(INIT_EVENTS);
  const [showChat, setShowChat] = useState(false);
  const [time, setTime] = useState(new Date());
  const [calYear, setCalYear] = useState(new Date().getFullYear());
  const [calMonth, setCalMonth] = useState(new Date().getMonth());
  const [selectedDay, setSelectedDay] = useState(new Date());
  const [calFilter, setCalFilter] = useState("all");

  useEffect(() => { const t = setInterval(()=>setTime(new Date()),1000); return ()=>clearInterval(t); }, []);

  const addEvent = (ev) => setEvents(prev => [...prev, ev]);
  const removeEvent = (id) => setEvents(prev => prev.filter(e=>e.id!==id));
  const toggle = (period, id) => setTodos(prev => ({ ...prev, [period]: prev[period].map(t=>t.id===id?{...t,done:!t.done}:t) }));

  const today = new Date();
  const hh = time.getHours().toString().padStart(2,"0");
  const mm = time.getMinutes().toString().padStart(2,"0");
  const weekdays = ["일","월","화","수","목","금","토"];
  const dateStr = `${today.getMonth()+1}월 ${today.getDate()}일 (${weekdays[today.getDay()]})`;
  const allTodos = [...todos.daily,...todos.weekly,...todos.monthly];
  const doneCount = allTodos.filter(t=>t.done).length;
  const totalPct = Math.round(doneCount/allTodos.length*100);

  // Exam alerts: within 60 days
  const examAlerts = events.filter(e => {
    if (!e.isExam) return false;
    const diff = daysBetween(today, new Date(e.date));
    return diff >= 0 && diff <= 60;
  }).sort((a,b)=>new Date(a.date)-new Date(b.date));

  // D-Days
  const ddays = [
    { label:"SQLD",    days:daysBetween(today,new Date("2026-07-10")), type:"work" },
    { label:"보험관리역", days:daysBetween(today,new Date("2026-07-27")), type:"work" },
    { label:"제주 여행", days:daysBetween(today,new Date("2026-08-10")), type:"personal" },
  ];

  // Selected day events
  const selEvs = events.filter(e => sameDay(new Date(e.date), selectedDay))
    .filter(e => calFilter==="all" || e.type===calFilter || (calFilter==="exam" && e.isExam));

  const navItems = [
    { id:"dashboard", icon:"home",     label:"홈" },
    { id:"todo",      icon:"check",    label:"할일" },
    { id:"goals",     icon:"target",   label:"목표" },
    { id:"calendar",  icon:"calendar", label:"캘린더" },
    { id:"ai",        icon:"ai",       label:"AI" },
  ];

  const ProgressBar = ({ value, color }) => (
    <div style={{ height:5, background:P.border, borderRadius:99, overflow:"hidden" }}>
      <div style={{ height:"100%", width:`${value}%`, background:color, borderRadius:99 }}/>
    </div>
  );

  const TodoRow = ({ t, period }) => (
    <div onClick={()=>toggle(period,t.id)}
      style={{ display:"flex", alignItems:"center", gap:11, padding:"12px 14px", cursor:"pointer", opacity:t.done?0.45:1, borderBottom:`1px solid ${P.border}` }}>
      <div style={{ width:22, height:22, borderRadius:7, border:`2px solid ${t.done?P.pink:"#e9d5ff"}`, background:t.done?P.pink:"#fff", display:"flex", alignItems:"center", justifyContent:"center", flexShrink:0 }}>
        {t.done && <svg width={11} height={11} viewBox="0 0 12 12"><path d="M2 6l3 3 5-5" stroke="#fff" strokeWidth={2.2} strokeLinecap="round" fill="none"/></svg>}
      </div>
      <span style={{ flex:1, fontSize:13.5, color:P.text, fontWeight:500, textDecoration:t.done?"line-through":"none" }}>{t.text}</span>
      <span style={{ fontSize:10, fontWeight:700, padding:"2px 8px", borderRadius:99, background:t.type==="work"?P.work.light:P.personal.light, color:t.type==="work"?P.work.text:P.personal.text, border:`1px solid ${t.type==="work"?P.work.border:P.personal.border}` }}>
        {t.type==="work"?"업무":"개인"}
      </span>
    </div>
  );

  const Card = ({ children, style={} }) => (
    <div style={{ background:P.card, borderRadius:16, border:`1px solid ${P.border}`, boxShadow:"0 2px 8px rgba(244,114,182,0.07)", ...style }}>{children}</div>
  );

  const monthName = ["1월","2월","3월","4월","5월","6월","7월","8월","9월","10월","11월","12월"];

  return (
    <div style={{ minHeight:"100vh", background:P.bg, fontFamily:"-apple-system,'SF Pro Text','Segoe UI',sans-serif", maxWidth:480, margin:"0 auto" }}>
      <style>{`
        *{box-sizing:border-box;margin:0;padding:0}
        ::-webkit-scrollbar{display:none}
        @keyframes up{from{opacity:0;transform:translateY(10px)}to{opacity:1;transform:translateY(0)}}
        .seg{flex:1;padding:7px 0;border:none;background:transparent;font-size:12px;font-weight:700;cursor:pointer;border-radius:10px;color:#9ca3af;transition:all .15s}
        .seg.on{background:#fff;color:#db2777;box-shadow:0 1px 4px rgba(244,114,182,.18)}
        .filt{padding:6px 13px;border-radius:99px;border:1.5px solid ${P.border};background:#fff;font-size:12px;font-weight:700;cursor:pointer;color:${P.sub};transition:all .15s;white-space:nowrap}
        .filt.on{border-color:${P.pink};background:${P.pinkLight};color:${P.pinkDark}}
      `}</style>

      {/* ─── DASHBOARD ─── */}
      {tab==="dashboard" && (
        <div style={{ paddingBottom:88, animation:"up 0.25s ease" }}>
          {/* Header */}
          <div style={{ padding:"52px 20px 22px", background:`linear-gradient(150deg,#f9a8d4 0%,${P.pink} 50%,${P.personal.main} 100%)` }}>
            <div style={{ fontSize:11, color:"rgba(255,255,255,0.75)", marginBottom:3 }}>{dateStr}</div>
            <div style={{ fontSize:44, fontWeight:800, color:"#fff", letterSpacing:"-2px", fontVariantNumeric:"tabular-nums", lineHeight:1 }}>{hh}:{mm}</div>
            {/* D-Days */}
            <div style={{ marginTop:16, display:"flex", gap:8, flexWrap:"wrap" }}>
              {ddays.filter(d=>d.days>=0).map((d,i) => (
                <div key={i} style={{ background:"rgba(255,255,255,0.22)", backdropFilter:"blur(10px)", borderRadius:12, padding:"8px 14px", border:"1px solid rgba(255,255,255,0.3)" }}>
                  <div style={{ fontSize:11, color:"rgba(255,255,255,0.7)", fontWeight:600 }}>{d.type==="work"?"업무":"개인"}</div>
                  <div style={{ display:"flex", alignItems:"center", gap:6 }}>
                    <span style={{ fontSize:17, fontWeight:900, color:"#fff" }}>D-{d.days}</span>
                    <span style={{ fontSize:11, color:"rgba(255,255,255,0.9)", fontWeight:700 }}>{d.label}</span>
                  </div>
                </div>
              ))}
            </div>
          </div>

          <div style={{ padding:"14px 14px 0" }}>

            {/* Exam Alert (60-day warning) */}
            {examAlerts.length>0 && (
              <Card style={{ padding:14, marginBottom:12, borderLeft:`4px solid ${P.exam.main}`, background:P.exam.light }}>
                <div style={{ display:"flex", alignItems:"center", gap:8, marginBottom:10 }}>
                  <Icon name="bell" size={15} color={P.exam.main} />
                  <span style={{ fontWeight:700, fontSize:13, color:P.exam.text }}>시험 일정 알림 (60일 이내)</span>
                </div>
                {examAlerts.map(e => {
                  const diff = daysBetween(today, new Date(e.date));
                  return (
                    <div key={e.id} style={{ display:"flex", alignItems:"center", justifyContent:"space-between", padding:"8px 10px", background:"#fff", borderRadius:10, marginBottom:6, border:`1px solid ${P.exam.border}` }}>
                      <div>
                        <div style={{ fontSize:13, fontWeight:700, color:P.text }}>{e.title}</div>
                        <div style={{ fontSize:11, color:P.sub, marginTop:1 }}>{fmtFull(new Date(e.date))} {e.regDate ? `· 접수: ${e.regDate}`:""}</div>
                      </div>
                      <span style={{ fontSize:13, fontWeight:900, color:diff<=14?P.exam.main:diff<=30?P.orange:P.pink, flexShrink:0, marginLeft:8 }}>D-{diff}</span>
                    </div>
                  );
                })}
              </Card>
            )}

            {/* AI Brief */}
            <Card style={{ padding:16, marginBottom:12, borderLeft:`4px solid ${P.pink}` }}>
              <div style={{ display:"flex", alignItems:"center", gap:8, marginBottom:10 }}>
                <div style={{ width:28, height:28, borderRadius:9, background:`linear-gradient(135deg,${P.pink},${P.personal.main})`, display:"flex", alignItems:"center", justifyContent:"center" }}>
                  <Icon name="ai" size={14} color="#fff" />
                </div>
                <span style={{ fontWeight:700, fontSize:14, color:P.text }}>오늘의 AI 브리핑</span>
                <button onClick={()=>setShowChat(true)} style={{ marginLeft:"auto", background:P.pinkLight, border:"none", borderRadius:8, padding:"4px 10px", fontSize:11, fontWeight:700, color:P.pinkDark, cursor:"pointer" }}>일정 추가 →</button>
              </div>
              <div style={{ background:P.pinkLight, borderRadius:10, padding:"12px 14px" }}>
                <p style={{ fontSize:13, lineHeight:1.85, color:"#4a1942" }}>
                  <strong style={{ color:P.work.text }}>📋 업무</strong> SQLD 시험까지 <strong>D-{ddays[0].days}</strong>! 오늘 보험교육 미팅이 있어요.<br/>
                  <strong style={{ color:P.personal.text }}>🌸 개인</strong> 오늘 수영 잊지 마세요. 이번주 러닝 달성 완료! 💪
                </p>
              </div>
            </Card>

            {/* Today Events */}
            <Card style={{ padding:16, marginBottom:12 }}>
              <div style={{ display:"flex", alignItems:"center", marginBottom:12 }}>
                <Icon name="calendar" size={16} color={P.pink} />
                <span style={{ fontWeight:700, fontSize:14, color:P.text, marginLeft:7 }}>오늘 일정</span>
                <div style={{ marginLeft:"auto", display:"flex", gap:8 }}>
                  <span style={{ fontSize:10, fontWeight:700, color:P.work.text, display:"flex", alignItems:"center", gap:3 }}><span style={{ width:8, height:8, borderRadius:2, background:P.work.main, display:"inline-block" }}/>업무</span>
                  <span style={{ fontSize:10, fontWeight:700, color:P.personal.text, display:"flex", alignItems:"center", gap:3 }}><span style={{ width:8, height:8, borderRadius:2, background:P.personal.main, display:"inline-block" }}/>개인</span>
                </div>
              </div>
              {events.filter(e=>sameDay(new Date(e.date),today)).length===0 && <div style={{ textAlign:"center", color:P.sub, fontSize:13, padding:"12px 0" }}>오늘 일정이 없어요 🌸</div>}
              <div style={{ display:"flex", flexDirection:"column", gap:7 }}>
                {events.filter(e=>sameDay(new Date(e.date),today)).map(e => {
                  const s = e.type==="work"?P.work:P.personal;
                  return (
                    <div key={e.id} style={{ display:"flex", alignItems:"center", gap:10, padding:"10px 12px", background:s.light, borderRadius:10, border:`1px solid ${s.border}` }}>
                      <div style={{ width:4, height:34, borderRadius:2, background:s.main, flexShrink:0 }}/>
                      <div style={{ fontSize:11, color:s.text, fontWeight:700, width:36, flexShrink:0 }}>{e.time}</div>
                      <div style={{ fontSize:13.5, fontWeight:600, color:P.text, flex:1 }}>{e.title}</div>
                    </div>
                  );
                })}
              </div>
            </Card>

            {/* Quick Todo */}
            <Card style={{ padding:16, marginBottom:12 }}>
              <div style={{ display:"flex", alignItems:"center", marginBottom:12 }}>
                <Icon name="check" size={16} color={P.pink} />
                <span style={{ fontWeight:700, fontSize:14, color:P.text, marginLeft:7 }}>오늘 할 일</span>
                <span style={{ marginLeft:"auto", fontSize:12, color:P.pink, fontWeight:800 }}>{doneCount}/{allTodos.length} 완료</span>
              </div>
              <ProgressBar value={totalPct} color={P.pink} />
              <div style={{ marginTop:10 }}>
                {todos.daily.slice(0,3).map(t => <TodoRow key={t.id} t={t} period="daily"/>)}
              </div>
              <button onClick={()=>setTab("todo")} style={{ width:"100%", marginTop:10, padding:9, background:P.pinkLight, border:`1px solid ${P.border}`, borderRadius:10, fontSize:12, color:P.pinkDark, fontWeight:700, cursor:"pointer" }}>전체 할일 보기 →</button>
            </Card>

            {/* Goals */}
            <Card style={{ padding:16, marginBottom:12 }}>
              <div style={{ display:"flex", alignItems:"center", marginBottom:14 }}>
                <Icon name="target" size={16} color={P.pink} />
                <span style={{ fontWeight:700, fontSize:14, color:P.text, marginLeft:7 }}>2026 목표</span>
              </div>
              {["work","personal"].map(type => (
                <div key={type} style={{ marginBottom:12 }}>
                  <div style={{ fontSize:11, fontWeight:800, color:type==="work"?P.work.text:P.personal.text, marginBottom:8, letterSpacing:"0.04em" }}>
                    {type==="work"?"📋 업무":"🌸 개인"}
                  </div>
                  {GOALS.filter(g=>g.type===type).map(g=>(
                    <div key={g.id} style={{ marginBottom:9 }}>
                      <div style={{ display:"flex", justifyContent:"space-between", marginBottom:5 }}>
                        <span style={{ fontSize:13, fontWeight:600, color:P.text }}>{g.label}</span>
                        <span style={{ fontSize:12, fontWeight:800, color:g.color }}>{g.progress}%</span>
                      </div>
                      <ProgressBar value={g.progress} color={g.color}/>
                    </div>
                  ))}
                </div>
              ))}
            </Card>
          </div>
        </div>
      )}

      {/* ─── TODO ─── */}
      {tab==="todo" && (
        <div style={{ paddingBottom:88, animation:"up 0.25s ease" }}>
          <div style={{ padding:"52px 20px 16px", background:"#fff", borderBottom:`1px solid ${P.border}` }}>
            <div style={{ fontSize:22, fontWeight:800, color:P.text }}>할 일</div>
            <div style={{ fontSize:13, color:P.sub, marginTop:2, marginBottom:14 }}>매일 · 매주 · 매달 기준 관리</div>
            <div style={{ display:"flex", background:P.pinkLight, borderRadius:12, padding:3 }}>
              {[{id:"daily",label:"매일"},{id:"weekly",label:"매주"},{id:"monthly",label:"매달"}].map(f=>(
                <button key={f.id} className={`seg${todoFilter===f.id?" on":""}`} onClick={()=>setTodoFilter(f.id)}>{f.label}</button>
              ))}
            </div>
          </div>
          <div style={{ padding:"12px 14px" }}>
            {["work","personal"].map(type => {
              const list = todos[todoFilter].filter(t=>t.type===type);
              const s = type==="work"?P.work:P.personal;
              return (
                <div key={type} style={{ marginBottom:14 }}>
                  <div style={{ fontSize:11, fontWeight:800, color:s.text, marginBottom:8, letterSpacing:"0.05em", display:"flex", alignItems:"center", gap:5 }}>
                    {type==="work"?"📋 업무":"🌸 개인"}
                    <span style={{ marginLeft:"auto", color:P.sub, fontWeight:600 }}>{list.filter(t=>t.done).length}/{list.length}</span>
                  </div>
                  <Card style={{ overflow:"hidden" }}>
                    {list.map((t,i) => (
                      <div key={t.id} onClick={()=>toggle(todoFilter,t.id)}
                        style={{ display:"flex", alignItems:"center", gap:11, padding:"13px 14px", cursor:"pointer", opacity:t.done?0.4:1, borderBottom:i<list.length-1?`1px solid ${P.border}`:"none", borderLeft:`3px solid ${s.main}` }}>
                        <div style={{ width:22, height:22, borderRadius:7, border:`2px solid ${t.done?s.main:P.border}`, background:t.done?s.main:"#fff", display:"flex", alignItems:"center", justifyContent:"center", flexShrink:0 }}>
                          {t.done && <svg width={11} height={11} viewBox="0 0 12 12"><path d="M2 6l3 3 5-5" stroke="#fff" strokeWidth={2.2} strokeLinecap="round" fill="none"/></svg>}
                        </div>
                        <span style={{ flex:1, fontSize:14, color:P.text, fontWeight:500, textDecoration:t.done?"line-through":"none" }}>{t.text}</span>
                      </div>
                    ))}
                  </Card>
                </div>
              );
            })}
          </div>
        </div>
      )}

      {/* ─── GOALS ─── */}
      {tab==="goals" && (
        <div style={{ paddingBottom:88, animation:"up 0.25s ease" }}>
          <div style={{ padding:"52px 20px 20px", background:"#fff", borderBottom:`1px solid ${P.border}` }}>
            <div style={{ fontSize:22, fontWeight:800, color:P.text }}>2026 목표</div>
            <div style={{ fontSize:13, color:P.sub, marginTop:2 }}>업무 · 개인 분리 관리</div>
          </div>
          <div style={{ padding:"12px 14px" }}>
            {["work","personal"].map(type=>(
              <div key={type} style={{ marginBottom:16 }}>
                <div style={{ fontSize:11, fontWeight:800, color:type==="work"?P.work.text:P.personal.text, marginBottom:9, letterSpacing:"0.05em" }}>
                  {type==="work"?"📋 업무 목표":"🌸 개인 목표"}
                </div>
                {GOALS.filter(g=>g.type===type).map(g=>(
                  <Card key={g.id} style={{ padding:16, marginBottom:10, borderLeft:`4px solid ${g.color}` }}>
                    <div style={{ display:"flex", justifyContent:"space-between", alignItems:"center", marginBottom:10 }}>
                      <div>
                        <div style={{ fontSize:15, fontWeight:700, color:P.text }}>{g.label}</div>
                        <div style={{ fontSize:11, color:P.sub, marginTop:2 }}>마감: {g.target}</div>
                      </div>
                      <div style={{ position:"relative", width:54, height:54, flexShrink:0 }}>
                        <svg width={54} height={54} style={{ transform:"rotate(-90deg)" }}>
                          <circle cx={27} cy={27} r={22} fill="none" stroke={P.border} strokeWidth={5}/>
                          <circle cx={27} cy={27} r={22} fill="none" stroke={g.color} strokeWidth={5} strokeDasharray={`${(g.progress/100)*138.2} 138.2`} strokeLinecap="round"/>
                        </svg>
                        <div style={{ position:"absolute", inset:0, display:"flex", alignItems:"center", justifyContent:"center", fontSize:11, fontWeight:900, color:g.color }}>{g.progress}%</div>
                      </div>
                    </div>
                    <ProgressBar value={g.progress} color={g.color}/>
                  </Card>
                ))}
              </div>
            ))}
          </div>
        </div>
      )}

      {/* ─── CALENDAR ─── */}
      {tab==="calendar" && (
        <div style={{ paddingBottom:88, animation:"up 0.25s ease" }}>
          {/* Month nav */}
          <div style={{ padding:"52px 20px 14px", background:"#fff", borderBottom:`1px solid ${P.border}` }}>
            <div style={{ display:"flex", alignItems:"center", justifyContent:"space-between", marginBottom:14 }}>
              <button onClick={()=>{ let y=calYear,m=calMonth-1; if(m<0){m=11;y--;} setCalYear(y);setCalMonth(m); }} style={{ width:34,height:34,borderRadius:"50%",border:`1px solid ${P.border}`,background:P.pinkLight,cursor:"pointer",display:"flex",alignItems:"center",justifyContent:"center" }}>
                <Icon name="chevL" size={16} color={P.pinkDark}/>
              </button>
              <span style={{ fontSize:18, fontWeight:800, color:P.text }}>{calYear}년 {monthName[calMonth]}</span>
              <button onClick={()=>{ let y=calYear,m=calMonth+1; if(m>11){m=0;y++;} setCalYear(y);setCalMonth(m); }} style={{ width:34,height:34,borderRadius:"50%",border:`1px solid ${P.border}`,background:P.pinkLight,cursor:"pointer",display:"flex",alignItems:"center",justifyContent:"center" }}>
                <Icon name="chevR" size={16} color={P.pinkDark}/>
              </button>
            </div>
            {/* Filter */}
            <div style={{ display:"flex", gap:6, overflowX:"auto", paddingBottom:4 }}>
              {[{id:"all",label:"전체"},{id:"work",label:"업무"},{id:"personal",label:"개인"},{id:"exam",label:"시험·접수"}].map(f=>(
                <button key={f.id} className={`filt${calFilter===f.id?" on":""}`} onClick={()=>setCalFilter(f.id)}>{f.label}</button>
              ))}
            </div>
          </div>

          <div style={{ padding:"0 14px" }}>
            {/* Calendar grid */}
            <Card style={{ padding:"10px 8px", marginTop:12, marginBottom:12 }}>
              <CalendarGrid year={calYear} month={calMonth}
                events={events.filter(e=>calFilter==="all"||e.type===calFilter||(calFilter==="exam"&&e.isExam))}
                onSelectDay={setSelectedDay} selectedDay={selectedDay}/>
            </Card>

            {/* Selected day detail */}
            <div style={{ marginBottom:12 }}>
              <div style={{ fontSize:13, fontWeight:700, color:P.text, marginBottom:9, display:"flex", alignItems:"center", gap:6 }}>
                <Icon name="calendar" size={14} color={P.pink}/>
                {selectedDay.getMonth()+1}월 {selectedDay.getDate()}일 일정
                <button onClick={()=>setShowChat(true)} style={{ marginLeft:"auto", background:P.pinkLight, border:`1px solid ${P.border}`, borderRadius:8, padding:"4px 10px", fontSize:11, fontWeight:700, color:P.pinkDark, cursor:"pointer", display:"flex", alignItems:"center", gap:4 }}>
                  <Icon name="plus" size={11} color={P.pinkDark}/> 추가
                </button>
              </div>

              {selEvs.length===0
                ? <Card style={{ padding:20, textAlign:"center" }}><div style={{ fontSize:13, color:P.sub }}>이 날 일정이 없어요 🌸</div><button onClick={()=>setShowChat(true)} style={{ marginTop:10, padding:"8px 18px", background:`linear-gradient(135deg,${P.pink},${P.personal.main})`, border:"none", borderRadius:10, color:"#fff", fontWeight:700, fontSize:12, cursor:"pointer" }}>AI로 일정 추가</button></Card>
                : selEvs.map(e=>{
                  const s = e.type==="work"?P.work:P.personal;
                  return (
                    <Card key={e.id} style={{ padding:"13px 14px", marginBottom:8, borderLeft:`4px solid ${s.main}`, background:s.light }}>
                      <div style={{ display:"flex", alignItems:"flex-start", justifyContent:"space-between" }}>
                        <div>
                          <div style={{ display:"flex", alignItems:"center", gap:6, marginBottom:3 }}>
                            <span style={{ fontSize:14, fontWeight:700, color:P.text }}>{e.title}</span>
                            {e.badge && <span style={{ fontSize:10, fontWeight:800, padding:"2px 7px", borderRadius:99, background:e.badge==="시험"?P.exam.light:e.badge==="접수"?"#fffbeb":"#f0fdf4", color:e.badge==="시험"?P.exam.main:e.badge==="접수"?P.orange:P.green, border:`1px solid ${e.badge==="시험"?P.exam.border:e.badge==="접수"?"#fde68a":"#bbf7d0"}` }}>{e.badge}</span>}
                          </div>
                          <div style={{ fontSize:11, color:P.sub }}>{e.time} · {e.type==="work"?"업무":"개인"}</div>
                          {e.isExam && e.regDate && <div style={{ fontSize:11, color:P.orange, fontWeight:600, marginTop:3 }}>📌 접수: {e.regDate}</div>}
                        </div>
                        <button onClick={()=>removeEvent(e.id)} style={{ background:"none", border:"none", cursor:"pointer", color:"#fca5a5", padding:4, flexShrink:0 }}>
                          <Icon name="trash" size={15} color="#fca5a5"/>
                        </button>
                      </div>
                    </Card>
                  );
                })}
            </div>

            {/* Exam schedule */}
            {(calFilter==="all"||calFilter==="exam") && (
              <Card style={{ padding:16, marginBottom:12 }}>
                <div style={{ fontWeight:700, fontSize:13, color:P.text, marginBottom:12, display:"flex", alignItems:"center", gap:6 }}>
                  <Icon name="bell" size={14} color={P.pink}/> 시험 일정표
                </div>
                {events.filter(e=>e.isExam).sort((a,b)=>new Date(a.date)-new Date(b.date)).map((e,i,arr)=>{
                  const diff = daysBetween(today, new Date(e.date));
                  const expired = diff < 0;
                  return (
                    <div key={e.id} style={{ padding:"12px 12px", borderRadius:12, marginBottom:i<arr.length-1?8:0, background:expired?"#f8fafc":P.exam.light, border:`1px solid ${expired?P.border:P.exam.border}`, opacity:expired?0.5:1 }}>
                      <div style={{ display:"flex", alignItems:"flex-start", justifyContent:"space-between" }}>
                        <div style={{ flex:1 }}>
                          <div style={{ fontSize:13.5, fontWeight:700, color:P.text, marginBottom:5 }}>{e.title}</div>
                          <div style={{ display:"flex", gap:12 }}>
                            <div><div style={{ fontSize:10, color:P.sub, fontWeight:600, marginBottom:1 }}>시험일</div><div style={{ fontSize:12, fontWeight:700, color:P.pinkDark }}>{fmtFull(new Date(e.date))}</div></div>
                            {e.regDate && <div><div style={{ fontSize:10, color:P.sub, fontWeight:600, marginBottom:1 }}>접수기간</div><div style={{ fontSize:11, fontWeight:600, color:"#475569" }}>{e.regDate}</div></div>}
                          </div>
                        </div>
                        <span style={{ fontSize:14, fontWeight:900, color:expired?"#94a3b8":diff<=14?P.exam.main:diff<=30?P.orange:P.pink, marginLeft:8, flexShrink:0 }}>{expired?"종료":`D-${diff}`}</span>
                      </div>
                    </div>
                  );
                })}
              </Card>
            )}
          </div>
        </div>
      )}

      {/* ─── AI Tab ─── */}
      {tab==="ai" && (
        <div style={{ paddingBottom:88, animation:"up 0.25s ease" }}>
          <div style={{ padding:"52px 20px 20px", background:"#fff", borderBottom:`1px solid ${P.border}` }}>
            <div style={{ fontSize:22, fontWeight:800, color:P.text }}>AI 비서</div>
            <div style={{ fontSize:13, color:P.sub, marginTop:2 }}>날짜 + 일정을 말하면 자동 등록해요</div>
          </div>
          <div style={{ padding:"20px 14px" }}>
            <Card style={{ padding:24, textAlign:"center", marginBottom:12 }}>
              <div style={{ width:68, height:68, borderRadius:"50%", background:`linear-gradient(135deg,${P.pink},${P.personal.main})`, display:"flex", alignItems:"center", justifyContent:"center", margin:"0 auto 14px" }}>
                <Icon name="ai" size={30} color="#fff"/>
              </div>
              <div style={{ fontWeight:800, fontSize:17, color:P.text, marginBottom:6 }}>AI 일정 비서 🌸</div>
              <div style={{ fontSize:13, color:P.sub, lineHeight:1.7 }}>날짜와 일정을 말하면<br/>캘린더에 자동으로 추가해드려요</div>
              <button onClick={()=>setShowChat(true)} style={{ marginTop:18, width:"100%", padding:14, background:`linear-gradient(135deg,${P.pink},${P.personal.main})`, border:"none", borderRadius:14, color:"#fff", fontWeight:700, fontSize:15, cursor:"pointer" }}>채팅 시작하기</button>
            </Card>
            <div style={{ fontSize:12, fontWeight:700, color:P.sub, marginBottom:8, marginLeft:2 }}>이렇게 말해보세요</div>
            {[
              "7월 20일 치과 예약 개인",
              "8월 5일 팀 워크숍 업무",
              "2026-09-01 AFPK 접수 업무",
              "이번주 해야할 것 정리해줘",
              "SQLD 시험까지 공부 계획 짜줘",
            ].map((q,i)=>(
              <button key={i} onClick={()=>setShowChat(true)} style={{ width:"100%", marginBottom:8, padding:"13px 16px", background:"#fff", border:`1px solid ${P.border}`, borderRadius:12, textAlign:"left", fontSize:13.5, color:P.text, fontWeight:500, cursor:"pointer", display:"flex", alignItems:"center", justifyContent:"space-between" }}>
                {q} <Icon name="chevR" size={14} color={P.sub}/>
              </button>
            ))}
          </div>
        </div>
      )}

      {/* ─── Bottom Nav ─── */}
      <div style={{ position:"fixed", bottom:0, left:"50%", transform:"translateX(-50%)", width:"100%", maxWidth:480, background:"rgba(255,255,255,0.97)", backdropFilter:"blur(20px)", borderTop:`1px solid ${P.border}`, display:"flex", paddingBottom:"env(safe-area-inset-bottom,8px)" }}>
        {navItems.map(n=>(
          <button key={n.id} onClick={()=>setTab(n.id)} style={{ flex:1, display:"flex", flexDirection:"column", alignItems:"center", gap:4, padding:"11px 0 7px", border:"none", background:"none", cursor:"pointer", color:tab===n.id?P.pink:P.sub }}>
            <Icon name={n.icon} size={22} color={tab===n.id?P.pink:P.sub}/>
            <span style={{ fontSize:10, fontWeight:700 }}>{n.label}</span>
            {tab===n.id && <span style={{ width:4, height:4, borderRadius:"50%", background:P.pink }}/>}
          </button>
        ))}
      </div>

      {showChat && <AIChat onClose={()=>setShowChat(false)} onAddEvent={addEvent}/>}
    </div>
  );
}
