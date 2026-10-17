<!doctype html>
<html lang="ar" dir="rtl">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>برنامج عروض الأسعار</title>
<style>
:root{--bg:#f3f4f6;--card:#fff;--ink:#1f2937;--mut:#6b7280;--line:#d1d5db;--pri:#1e3a5f;--danger:#b91c1c}
*{box-sizing:border-box}
body{margin:0;font-family:"Segoe UI",Tahoma,Arial,sans-serif;background:var(--bg);color:var(--ink);font-size:15px}
header{background:var(--pri);color:#fff;padding:10px 20px;display:flex;gap:8px;align-items:center;flex-wrap:wrap}
header h1{font-size:18px;margin:0 0 0 20px}
.tab{background:transparent;border:1px solid rgba(255,255,255,.4);color:#fff;padding:6px 14px;border-radius:6px;cursor:pointer;font:inherit}
.tab.on{background:#fff;color:var(--pri)}
main{padding:16px;max-width:1500px;margin:auto}
.view{display:none}.view.on{display:block}
.grid{display:grid;grid-template-columns:minmax(380px,540px) 1fr;gap:16px;align-items:start}
.grid>*{min-width:0}
@media(max-width:1000px){.grid{grid-template-columns:1fr}}
.card{background:var(--card);border:1px solid var(--line);border-radius:10px;padding:14px}
label{display:block;font-size:13px;color:var(--mut);margin:10px 0 3px}
input,select,textarea{width:100%;padding:7px 9px;border:1px solid var(--line);border-radius:6px;font:inherit;background:#fff;color:var(--ink)}
input[type=checkbox],input[type=radio]{width:auto}
input[type=range]{padding:0}
textarea{min-height:60px;resize:vertical}
.row{display:flex;gap:10px;align-items:center}.row>*{flex:1}
button.b{background:var(--pri);color:#fff;border:0;padding:8px 14px;border-radius:6px;cursor:pointer;font:inherit}
button.b.sec{background:#e5e7eb;color:var(--ink)}
button.b.red{background:var(--danger)}
button.b.sm{padding:4px 9px;font-size:13px}
.types{display:flex;gap:6px}
.types label{flex:1;margin:0;border:1px solid var(--line);border-radius:6px;padding:8px;text-align:center;cursor:pointer;color:var(--ink)}
.types input{display:none}
.types label:has(input:checked){border-color:var(--pri);background:#eaf1fb;font-weight:700;color:var(--pri)}
.items .it{border:1px solid var(--line);border-radius:8px;padding:8px;margin-top:8px;background:#fafafa}
.it .row{margin-top:6px}
.it textarea{margin-top:6px;min-height:44px}
.thumb{max-height:46px;max-width:70px;border:1px solid var(--line);border-radius:4px}
.chk{display:flex;gap:6px;align-items:center;margin:10px 0 0;color:var(--ink);font-size:14px}
.chk label{margin:0 0 0 12px;color:var(--ink);display:flex;gap:4px;align-items:center}
.trm{display:flex;gap:6px;align-items:center;padding:5px 0;border-bottom:1px dashed var(--line);flex-wrap:wrap}
.trm input.ti{width:70px;padding:2px 5px;display:inline-block}
.trm input.tt{width:200px;padding:2px 5px;display:inline-block}
.sticky{position:sticky;top:10px}
table.list{width:100%;border-collapse:collapse}
table.list th,table.list td{padding:8px;border-bottom:1px solid var(--line);text-align:right}
table.list th{background:#f9fafb}
.actions{display:flex;gap:6px;flex-wrap:wrap;align-items:center}
.hint{font-size:12px;color:var(--mut);margin-top:4px}
.refbox{font-weight:700;direction:ltr;text-align:center;letter-spacing:1px}
.box{border:1px dashed var(--line);border-radius:8px;padding:10px;margin-top:10px}
.box img{max-width:100%;max-height:120px;display:block;margin:6px 0}
.rg{display:flex;gap:8px;align-items:center;margin-top:6px}
.rg span{flex:0 0 150px;font-size:13px}
.rg output{flex:0 0 42px;text-align:center;font-weight:700;font-size:13px}
.rg input:disabled{opacity:.4}

/* الورقة */
.paper{background:#fff;border:1px solid var(--line);box-shadow:0 2px 10px rgba(0,0,0,.08);width:210mm;margin:auto;
  --lh:1.7;--fs:14px;--rp:6px;--gap:11px;--sig:28px}
.paper .cnt{line-height:var(--lh);font-size:var(--fs)}
.paper .blk{margin:0 0 var(--gap)}
.paper .intro p{margin:0 0 .35em}
.paper table.pg{width:100%;height:297mm;border-collapse:collapse}
.paper table.pg>thead>tr>td,.paper table.pg>tbody>tr>td,.paper table.pg>tfoot>tr>td{border:0;padding:0;text-align:start}
.paper td.hd img.hf,.paper td.ft img.hf{width:100%;display:block}
.paper table.pg>tbody>tr>td.bd{padding:9mm 20mm 7mm;vertical-align:top;height:100%}
.paper .co{text-align:center;border-bottom:3px double var(--pri);padding:12px 20mm 8px;margin-bottom:6px}
.paper .co h2{margin:0;color:var(--pri);font-size:24px}
.paper .co div{color:var(--mut);font-size:12px;white-space:pre-line}
.paper .meta{display:flex;justify-content:space-between;border-bottom:1px solid #bbb;padding-bottom:6px;margin-bottom:calc(var(--gap)*1.2)}
.paper .meta bdi{font-weight:700}
.paper .addr{font-size:1.08em}
.paper .subj b{border-bottom:1px solid var(--ink)}
.itbl{width:100%;border-collapse:collapse;margin:var(--gap) 0}
.itbl th,.itbl td{border:1px solid #444;padding:var(--rp) 8px;text-align:center}
.itbl th{background:#e8eef6}
.itbl td.l{text-align:start}
.itbl td.l small{display:block;color:#444;white-space:pre-line}
.itbl td img{max-width:80px;max-height:70px;display:block;margin:auto}
.itbl .tot td{font-weight:700;background:#f5f7fa}
.paper h4{margin:var(--gap) 0 4px;color:var(--pri);font-size:1.05em}
.paper ol{margin:2px 0;padding-inline-start:22px}
.paper ol li{margin-bottom:calc(var(--gap)*.25)}
.paper .sig{margin-top:var(--sig)}
@media print{
  body{background:#fff}
  header,.no-print,.editor{display:none!important}
  main{padding:0;max-width:none}
  .grid{display:block}
  .paper{border:0;box-shadow:none;width:210mm;zoom:1!important}
  .paper table.pg{height:296mm}
  .sticky{position:static}
  thead{display:table-header-group}
  tfoot{display:table-footer-group}
  tr{break-inside:avoid}
  @page{size:A4;margin:0}
}
</style>
</head>
<body>
<header class="no-print">
  <h1>برنامج عروض الأسعار</h1>
  <button class="tab on" data-v="edit">عرض جديد / تعديل</button>
  <button class="tab" data-v="list">العروض المحفوظة</button>
  <button class="tab" data-v="set">الإعدادات</button>
</header>

<main>
<!-- المحرر -->
<section id="v-edit" class="view on">
 <div class="grid">
  <div class="editor card">
    <div class="types" id="types">
      <label><input type="radio" name="type" value="price"><span>عرض سعر عادي</span></label>
      <label><input type="radio" name="type" value="financial"><span>عرض مالي</span></label>
      <label><input type="radio" name="type" value="technical"><span>عرض فني</span></label>
    </div>

    <div class="row">
      <div><label>رقم الإشارة</label><input id="ref" class="refbox"></div>
      <div><label>التاريخ</label><input id="date" type="date"></div>
      <div><label>لغة العرض</label><select id="lang"><option value="ar">عربي</option><option value="en">English</option></select></div>
    </div>

    <label>اسم العميل</label>
    <input id="client" list="clientsList" placeholder="اكتب اسم الشركة (يُحفظ تلقائياً)">
    <datalist id="clientsList"></datalist>

    <div class="row">
      <div><label>الموضوع</label><input id="subject" placeholder="مثال: عرض سعر لتوريد ..."></div>
      <div><label>كلمة عن المحتوى (لاسم الملف)</label><input id="fileWord" placeholder="مثال: لوحات"></div>
    </div>
    <div class="hint" id="fileHint"></div>

    <label>مقدمة العرض</label>
    <textarea id="intro"></textarea>

    <label>البنود</label>
    <label class="chk"><input type="checkbox" id="showImgs"> إضافة صور للبنود (لهذا العرض فقط)</label>
    <div class="items" id="items"></div>
    <button class="b sec sm" style="margin-top:8px" onclick="addItem()">+ إضافة بند</button>
    <div class="row" id="taxRow" style="margin-top:6px">
      <div><label>ضريبة المبيعات % (تُحسب في الجدول)</label><input id="tax" type="number" min="0" step="0.01"></div>
      <div><label>خصم (مبلغ)</label><input id="discount" type="number" min="0" step="0.001"></div>
    </div>

    <label style="margin-top:14px">الملاحظات (اختر ما يناسب)</label>
    <div id="terms"></div>
    <label>ملاحظات أخرى (نص حر)</label>
    <textarea id="customTerms" placeholder="سطر لكل ملاحظة"></textarea>

    <label>اسم معدّ العرض (للتوقيع)</label>
    <input id="preparer">

    <details class="box" id="fmtBox">
      <summary style="cursor:pointer;font-weight:700">🎛️ التنسيق والخطوط</summary>
      <div class="chk">
        <label><input type="radio" name="fmtmode" value="auto"> تلقائي</label>
        <label><input type="radio" name="fmtmode" value="manual"> يدوي</label>
      </div>
      <div class="hint">التلقائي يضبط المسافات حسب طول العرض. اليدوي تتحكم أنت بالأحجام والمسافات. الخط والإزاحة والهوامش تعمل في الحالتين.</div>
      <label>نوع الخط</label>
      <select id="fmt_font"></select>
      <div id="fmtRanges"></div>
      <button class="b sec sm" style="margin-top:10px" onclick="resetFmt()">إعادة الضبط الافتراضي</button>
    </details>

    <div class="actions" style="margin-top:14px">
      <button class="b" onclick="saveQuote()">💾 حفظ</button>
      <button class="b sec" onclick="window.print()">🖨️ طباعة / PDF</button>
      <button class="b sec" onclick="exportWord()">📄 تصدير Word</button>
      <button class="b sec" onclick="newQuote()">+ عرض جديد</button>
    </div>
    <div class="box">
      <div style="font-size:13px;margin-bottom:6px">إنشاء عرض جديد بنفس المعلومات (يحفظ الحالي أولاً):</div>
      <div class="row">
        <select id="convType">
          <option value="technical">عرض فني</option>
          <option value="financial">عرض مالي</option>
          <option value="price">عرض سعر عادي</option>
        </select>
        <button class="b sec" style="flex:0 0 auto" onclick="convertTo()">إنشاء</button>
      </div>
    </div>
    <div class="hint" id="saveMsg"></div>
  </div>

  <div class="sticky"><div class="paper" id="paper"></div></div>
 </div>
</section>

<!-- القائمة -->
<section id="v-list" class="view">
  <div class="card">
    <input id="q" placeholder="بحث باسم العميل أو رقم الإشارة أو الموضوع" style="max-width:420px;margin-bottom:10px">
    <table class="list"><thead><tr><th>الرقم</th><th>التاريخ</th><th>العميل</th><th>النوع</th><th>الإجمالي</th><th></th></tr></thead>
    <tbody id="listBody"></tbody></table>
    <div class="hint" id="emptyMsg"></div>
  </div>
</section>

<!-- الإعدادات -->
<section id="v-set" class="view">
  <div class="card" style="max-width:680px">
    <h3 style="margin-top:0">الترقيم</h3>
    <div class="row">
      <div><label>رقم العرض التالي (البداية)</label><input id="s_next" type="number" min="1"></div>
      <div><label>حرف المعدّ</label><input id="s_letter" maxlength="2" placeholder="ل"></div>
    </div>
    <label>اسم المعدّ الافتراضي (للتوقيع)</label><input id="s_prep">
    <div class="hint">الرقم يظهر بالشكل (السنة/الرقم/الحرف) مثل <b dir="ltr">26/187/ل</b> ويزيد تلقائياً بعد كل عرض جديد يُحفظ.</div>

    <h3>الرأس والتذييل (صور)</h3>
    <div class="box">
      <b>صورة الرأس (Header)</b>
      <div class="hint">يفضّل عرض 1600 بكسل تقريباً وارتفاع قليل. تظهر أعلى الصفحة.</div>
      <img id="p_head" style="display:none">
      <div class="actions"><input type="file" accept="image/*" onchange="setHF('headerImg',this)" style="flex:1">
      <button class="b red sm" onclick="clearHF('headerImg')">حذف</button></div>
    </div>
    <div class="box">
      <b>صورة التذييل (Footer)</b>
      <div class="hint">تظهر أسفل كل صفحة.</div>
      <img id="p_foot" style="display:none">
      <div class="actions"><input type="file" accept="image/*" onchange="setHF('footerImg',this)" style="flex:1">
      <button class="b red sm" onclick="clearHF('footerImg')">حذف</button></div>
    </div>
    <div class="hint">إذا لم ترفع صورة رأس، يُستخدم الاسم والبيانات النصية التالية بدلاً منها:</div>
    <label>اسم الشركة</label><input id="s_co">
    <label>عنوان / هاتف / بريد (سطر لكل معلومة)</label><textarea id="s_coinfo"></textarea>

    <h3>أخرى</h3>
    <div class="row">
      <div><label>العملة (عربي)</label><input id="s_cur"></div>
      <div><label>العملة (English)</label><input id="s_curen" placeholder="JOD"></div>
    </div>
    <div class="row">
      <div><label>عدد الخانات العشرية</label><input id="s_dec" type="number" min="0" max="3"></div>
      <div><label>الضريبة الافتراضية في الجدول %</label><input id="s_tax" type="number" min="0" step="0.01"></div>
    </div>
    <div class="actions" style="margin-top:14px">
      <button class="b" onclick="saveSettings()">حفظ الإعدادات</button>
    </div>
    <hr style="margin:20px 0">
    <h3>نسخة احتياطية</h3>
    <div class="hint">البيانات (والصور) محفوظة داخل المتصفح على هذا الجهاز. خذ نسخة احتياطية بين فترة وأخرى.</div>
    <div class="actions" style="margin-top:8px">
      <button class="b sec" onclick="exportData()">تصدير نسخة (JSON)</button>
      <button class="b sec" onclick="document.getElementById('imp').click()">استيراد نسخة</button>
      <input type="file" id="imp" accept=".json" style="display:none" onchange="importData(event)">
    </div>
  </div>
</section>
</main>

<script>
/*CORE_START*/
const I18N={
 ar:{ref:'الرقم',date:'التاريخ',to:c=>`السادة / ${c||'.........'} المحترمين`,subject:'الموضوع',no:'#',desc:'الوصف',img:'الصورة',unit:'الوحدة',qty:'الكمية',price:'السعر',total:'الإجمالي',sub:'المجموع',disc:'الخصم',tax:r=>`ضريبة المبيعات ${r}%`,grand:c=>`الإجمالي النهائي (${c})`,notes:'ملاحظات:',close:'وتفضلوا بقبول فائق الاحترام ،،،'},
 en:{ref:'Ref',date:'Date',to:c=>`To: ${c||'.........'}`,subject:'Subject',no:'#',desc:'Description',img:'Image',unit:'Unit',qty:'Qty',price:'Unit Price',total:'Total',sub:'Subtotal',disc:'Discount',tax:r=>`Sales Tax ${r}%`,grand:c=>`Grand Total (${c})`,notes:'Notes:',close:'Best regards,'}
};
/* كتالوج الملاحظات الجاهزة: t = عربي، e = English، {x} حقل قابل للتعديل، ex = خيار يلغي الآخر */
const TERM_CAT=[
 {k:'validity',t:'صلاحية العرض {n} يوماً من تاريخه',e:'This offer is valid for {n} days from its date',f:{n:30}},
 {k:'tax_add',t:'يضاف للأسعار الضريبة العامة على المبيعات {r}%',e:'General Sales Tax of {r}% will be added to the prices',f:{r:16},ex:'tax_incl'},
 {k:'tax_incl',t:'الأسعار أعلاه تشمل ضريبة المبيعات {r}%',e:'The above prices include General Sales Tax of {r}%',f:{r:16},ex:'tax_add'},
 {k:'deliv_incl',t:'الأسعار أعلاه تشمل التوصيل',e:'The above prices include delivery',f:{},ex:'deliv_excl'},
 {k:'deliv_excl',t:'الأسعار أعلاه لا تشمل التوصيل',e:'The above prices do not include delivery',f:{},ex:'deliv_incl'},
 {k:'delivery',t:'التسليم خلال {a} إلى {b} يوم عمل من تاريخ إشعارنا',e:'Delivery within {a} to {b} working days from the date of our notification',f:{a:45,b:60}},
 {k:'payment',t:'شروط الدفع: {p}',e:'Payment terms: {p}',f:{p:'دفعة مقدمة 50% والباقي عند التسليم'},fe:{p:'50% advance payment, balance upon delivery'}},
 {k:'warranty',t:'الكفالة: {w}',e:'Warranty: {w}',f:{w:'سنة واحدة'},fe:{w:'One year'}}
];
function termLinesPlain(q){
  const en=q.lang==='en';
  return TERM_CAT.filter(c=>q.terms[c.k].on)
    .map(c=>(en?c.e:c.t).replace(/\{(\w+)\}/g,(m,n)=>q.terms[c.k].v[n]))
    .concat(String(q.customTerms||'').split('\n').map(x=>x.trim()).filter(Boolean));
}
function totals(q){
  const sub=(q.items||[]).reduce((a,it)=>a+(it.qty||0)*(it.price||0),0);
  const after=Math.max(sub-(q.discount||0),0);
  const tax=after*(q.tax||0)/100;
  return {sub,after,tax,total:after+tax};
}
const fmt=n=>Number(n).toLocaleString('en-US',{minimumFractionDigits:db.settings.decimals,maximumFractionDigits:db.settings.decimals});
/*CORE_END*/

/*DOCX_START*/
/* ---- مولّد ملف Word (docx) بدون مكتبات خارجية ---- */
const XE=s=>String(s??'').replace(/[&<>"]/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;'}[c]));
const CRC_T=(()=>{const t=new Uint32Array(256);for(let n=0;n<256;n++){let c=n;for(let k=0;k<8;k++)c=c&1?0xEDB88320^(c>>>1):c>>>1;t[n]=c>>>0}return t})();
function crc32(u8){let c=0xFFFFFFFF;for(let i=0;i<u8.length;i++)c=CRC_T[(c^u8[i])&255]^(c>>>8);return (c^0xFFFFFFFF)>>>0}
function zipStore(files){
  const enc=new TextEncoder();let off=0;const parts=[],cd=[];
  files.forEach(f=>{
    const nm=enc.encode(f.name),crc=crc32(f.data),sz=f.data.length;
    const lh=new DataView(new ArrayBuffer(30));
    lh.setUint32(0,0x04034b50,true);lh.setUint16(4,20,true);lh.setUint16(6,0x0800,true);lh.setUint16(8,0,true);
    lh.setUint16(10,0,true);lh.setUint16(12,33,true);lh.setUint32(14,crc,true);lh.setUint32(18,sz,true);
    lh.setUint32(22,sz,true);lh.setUint16(26,nm.length,true);lh.setUint16(28,0,true);
    parts.push(new Uint8Array(lh.buffer),nm,f.data);
    const ch=new DataView(new ArrayBuffer(46));
    ch.setUint32(0,0x02014b50,true);ch.setUint16(4,20,true);ch.setUint16(6,20,true);ch.setUint16(8,0x0800,true);
    ch.setUint16(10,0,true);ch.setUint16(12,0,true);ch.setUint16(14,33,true);ch.setUint32(16,crc,true);
    ch.setUint32(20,sz,true);ch.setUint32(24,sz,true);ch.setUint16(28,nm.length,true);
    ch.setUint32(42,off,true);
    cd.push(new Uint8Array(ch.buffer),nm);
    off+=30+nm.length+sz;
  });
  const cdSize=cd.reduce((a,b)=>a+b.length,0);
  const e=new DataView(new ArrayBuffer(22));
  e.setUint32(0,0x06054b50,true);e.setUint16(8,files.length,true);e.setUint16(10,files.length,true);
  e.setUint32(12,cdSize,true);e.setUint32(16,off,true);
  return new Blob([...parts,...cd,new Uint8Array(e.buffer)],{type:'application/vnd.openxmlformats-officedocument.wordprocessingml.document'});
}
function dataUrlBytes(u){const b=atob(u.split(',')[1]);const a=new Uint8Array(b.length);for(let i=0;i<b.length;i++)a[i]=b.charCodeAt(i);return a}
function imgInfo(b){
  if(b[0]===0x89&&b[1]===0x50)return{ext:'png',w:((b[16]<<24)|(b[17]<<16)|(b[18]<<8)|b[19])>>>0,h:((b[20]<<24)|(b[21]<<16)|(b[22]<<8)|b[23])>>>0};
  let i=2;
  while(i<b.length-9){
    if(b[i]!==0xFF){i++;continue}
    const m=b[i+1];
    if(m>=0xC0&&m<=0xCF&&m!==0xC4&&m!==0xC8&&m!==0xCC)return{ext:'jpeg',h:(b[i+5]<<8)|b[i+6],w:(b[i+7]<<8)|b[i+8]};
    i+=2+((b[i+2]<<8)|b[i+3]);
  }
  return{ext:'jpeg',w:4,h:3};
}
const NS='xmlns:w="http://schemas.openxmlformats.org/wordprocessingml/2006/main" xmlns:r="http://schemas.openxmlformats.org/officeDocument/2006/relationships" xmlns:wp="http://schemas.openxmlformats.org/drawingml/2006/wordprocessingDrawing" xmlns:a="http://schemas.openxmlformats.org/drawingml/2006/main" xmlns:pic="http://schemas.openxmlformats.org/drawingml/2006/picture"';
const XMLH='<?xml version="1.0" encoding="UTF-8" standalone="yes"?>';

function buildDocx(q,s,L,tx){
  const ar=q.lang!=='en',f=q.fmt,font=XE(f.font),tech=q.type==='technical';
  const files=[],docRels=[],hdrRels=[],ftrRels=[];let imgN=0,docPrId=1;
  const fsHalf=Math.round(L.fs*1.5),lineAuto=Math.round(L.lh/1.2*240),gapTw=Math.round(L.gap*15),rpTw=Math.round(L.rp*15),sigTw=Math.round(L.sig*15);
  const sideTw=Math.round(f.side*56.7),topTw=Math.max(20,Math.round((9+f.top)*56.7));
  const contentW=11906-2*sideTw;
  const REL='http://schemas.openxmlformats.org/officeDocument/2006/relationships';

  function addImg(url,rels){
    const bytes=dataUrlBytes(url),info=imgInfo(bytes);imgN++;
    const name='media/img'+imgN+'.'+info.ext,id='rId'+(rels.length+10);
    files.push({name:'word/'+name,data:bytes});
    rels.push(`<Relationship Id="${id}" Type="${REL}/image" Target="${name}"/>`);
    return{id,info};
  }
  function drawing(id,cx,cy){
    const n=docPrId++;
    return `<w:r><w:drawing><wp:inline distT="0" distB="0" distL="0" distR="0"><wp:extent cx="${cx}" cy="${cy}"/><wp:docPr id="${n}" name="Picture ${n}"/><wp:cNvGraphicFramePr><a:graphicFrameLocks noChangeAspect="1"/></wp:cNvGraphicFramePr><a:graphic><a:graphicData uri="http://schemas.openxmlformats.org/drawingml/2006/picture"><pic:pic><pic:nvPicPr><pic:cNvPr id="${n}" name="img${n}"/><pic:cNvPicPr/></pic:nvPicPr><pic:blipFill><a:blip r:embed="${id}"/><a:stretch><a:fillRect/></a:stretch></pic:blipFill><pic:spPr><a:xfrm><a:off x="0" y="0"/><a:ext cx="${cx}" cy="${cy}"/></a:xfrm><a:prstGeom prst="rect"><a:avLst/></a:prstGeom></pic:spPr></pic:pic></a:graphicData></a:graphic></wp:inline></w:drawing></w:r>`;
  }
  const rPr=(o={})=>`<w:rPr><w:rFonts w:ascii="${font}" w:hAnsi="${font}" w:cs="${font}" w:eastAsia="${font}"/>${o.b?'<w:b/><w:bCs/>':''}${o.color?`<w:color w:val="${o.color}"/>`:''}<w:sz w:val="${o.sz||fsHalf}"/><w:szCs w:val="${o.sz||fsHalf}"/>${o.u?'<w:u w:val="single"/>':''}${ar&&!o.nortl?'<w:rtl/>':''}</w:rPr>`;
  function run(text,o){
    const segs=String(text??'').split('\n');
    return `<w:r>${rPr(o)}${segs.map((t,i)=>(i?'<w:br/>':'')+`<w:t xml:space="preserve">${XE(t)}</w:t>`).join('')}</w:r>`;
  }
  function para(inner,o={}){
    return `<w:p><w:pPr>${o.bdr?`<w:pBdr><w:bottom w:val="${o.bdr.v||'single'}" w:sz="${o.bdr.sz}" w:space="1" w:color="${o.bdr.c}"/></w:pBdr>`:''}${ar?'<w:bidi/>':''}<w:spacing w:before="${o.before||0}" w:after="${o.after||0}" w:line="${o.line||lineAuto}" w:lineRule="${o.rule||'auto'}"/>${o.ind||''}${o.jc?`<w:jc w:val="${o.jc}"/>`:''}</w:pPr>${inner}</w:p>`;
  }
  const bord=(c,sz)=>['top','left','bottom','right','insideH','insideV'].map(k=>`<w:${k} w:val="single" w:sz="${sz}" w:space="0" w:color="${c}"/>`).join('');
  function cell(w,content,o={}){
    return `<w:tc><w:tcPr><w:tcW w:w="${w}" w:type="dxa"/>${o.span?`<w:gridSpan w:val="${o.span}"/>`:''}${o.fill?`<w:shd w:val="clear" w:color="auto" w:fill="${o.fill}"/>`:''}<w:tcMar><w:top w:w="${rpTw}" w:type="dxa"/><w:left w:w="100" w:type="dxa"/><w:bottom w:w="${rpTw}" w:type="dxa"/><w:right w:w="100" w:type="dxa"/></w:tcMar><w:vAlign w:val="center"/></w:tcPr>${content}</w:tc>`;
  }
  const tx_=(t,o)=>para(run(t,o),{jc:'center',line:240});

  /* ---------- الرأس ---------- */
  let hdrXml='';
  if(s.headerImg){
    const im=addImg(s.headerImg,hdrRels),cx=7560000,cy=Math.round(cx*im.info.h/im.info.w);
    hdrXml=`<w:p><w:pPr><w:spacing w:before="0" w:after="0" w:line="240" w:lineRule="auto"/><w:ind w:left="${-sideTw}" w:right="${-sideTw}"/></w:pPr>${drawing(im.id,cx,cy)}</w:p>`;
  }else if(s.company||s.companyInfo){
    hdrXml=para(run(s.company||'',{b:1,sz:48,color:'1E3A5F'}),{jc:'center',line:240})+
      String(s.companyInfo||'').split('\n').filter(Boolean).map(l=>para(run(l,{sz:22,color:'6B7280'}),{jc:'center',line:240})).join('')+
      para('',{line:120,rule:'exact',bdr:{v:'double',sz:12,c:'1E3A5F'}});
  }
  /* ---------- التذييل ---------- */
  let ftrXml='';
  if(s.footerImg){
    const im=addImg(s.footerImg,ftrRels),cx=7560000,cy=Math.round(cx*im.info.h/im.info.w);
    ftrXml=`<w:p><w:pPr><w:spacing w:before="0" w:after="0" w:line="240" w:lineRule="auto"/><w:ind w:left="${-sideTw}" w:right="${-sideTw}"/></w:pPr>${drawing(im.id,cx,cy)}</w:p>`;
  }

  /* ---------- الجسم ---------- */
  const body=[];
  body.push(para('',{before:topTw,line:20,rule:'exact'}));
  // الرقم والتاريخ
  const half=Math.floor(contentW/2);
  const refTxt='\u202A('+q.ref+')\u202C',dateTxt='\u202A'+q.date+'\u202C';
  body.push(`<w:tbl><w:tblPr>${ar?'<w:bidiVisual/>':''}<w:tblW w:w="${contentW}" w:type="dxa"/><w:tblBorders><w:bottom w:val="single" w:sz="6" w:space="0" w:color="BBBBBB"/></w:tblBorders><w:tblLayout w:type="fixed"/></w:tblPr><w:tblGrid><w:gridCol w:w="${half}"/><w:gridCol w:w="${contentW-half}"/></w:tblGrid><w:tr>`+
    cell(half,para(run(tx.ref+': ')+run(refTxt,{b:1,nortl:1})),{})+
    cell(contentW-half,para(run(tx.date+': ')+run(dateTxt,{b:1,nortl:1}),{jc:'right'}),{})+
    `</w:tr></w:tbl>`);
  body.push(para(run(tx.to(q.client),{b:1,sz:Math.round(fsHalf*1.08)}),{before:Math.round(gapTw*1.2),after:gapTw}));
  if(q.subject)body.push(para(run(tx.subject+': ')+run(q.subject,{b:1,u:1}),{after:gapTw}));
  const introLines=String(q.intro||'').split('\n').map(x=>x.trim()).filter(Boolean);
  introLines.forEach((l,i)=>body.push(para(run(l),{after:i===introLines.length-1?gapTw:90})));

  // جدول البنود
  const img=!!q.showImgs;
  const fixed={no:520,unit:1000,qty:900,img:1500,price:1300,total:1400};
  const cols=['no','desc'].concat(img?['img']:[]).concat(['unit','qty']).concat(tech?[]:['price','total']);
  let used=0;cols.forEach(c=>{if(c!=='desc')used+=fixed[c]});
  const W={...fixed,desc:contentW-used};
  const n=cols.length;
  const hdrCell=c=>cell(W[c],para(run(tx[c],{b:1}),{jc:'center',line:240}),{fill:'E8EEF6'});
  let tbl=`<w:tbl><w:tblPr>${ar?'<w:bidiVisual/>':''}<w:tblW w:w="${contentW}" w:type="dxa"/><w:tblBorders>${bord('444444',4)}</w:tblBorders><w:tblLayout w:type="fixed"/></w:tblPr><w:tblGrid>${cols.map(c=>`<w:gridCol w:w="${W[c]}"/>`).join('')}</w:tblGrid>`;
  tbl+=`<w:tr><w:trPr><w:cantSplit/><w:tblHeader/></w:trPr>${cols.map(hdrCell).join('')}</w:tr>`;
  q.items.forEach((it,i)=>{
    const cs=[];
    cs.push(cell(W.no,tx_(String(i+1))));
    let d=para(run(it.desc),{line:240});
    if(it.spec)d+=para(run(it.spec,{sz:Math.round(fsHalf*.86),color:'444444'}),{line:240});
    cs.push(cell(W.desc,d));
    if(img){
      let c='';
      if(it.img){
        const im=addImg(it.img,docRels),sc=Math.min(80/im.info.w,70/im.info.h,1);
        c=para(drawing(im.id,Math.round(im.info.w*sc*9525),Math.round(im.info.h*sc*9525)),{jc:'center',line:240});
      }else c=para('',{line:240});
      cs.push(cell(W.img,c));
    }
    cs.push(cell(W.unit,tx_(it.unit)));
    cs.push(cell(W.qty,tx_(String(it.qty))));
    if(!tech){
      cs.push(cell(W.price,tx_(fmt(it.price))));
      cs.push(cell(W.total,tx_(fmt(it.qty*it.price))));
    }
    tbl+=`<w:tr><w:trPr><w:cantSplit/></w:trPr>${cs.join('')}</w:tr>`;
  });
  if(!tech){
    const t=totals(q),cur=ar?(s.currency||''):(s.currencyEn||'JOD');
    const span=n-1,spanW=contentW-W.total;
    const trow=(label,val)=>`<w:tr><w:trPr><w:cantSplit/></w:trPr>${cell(spanW,tx_(label,{b:1}),{span,fill:'F5F7FA'})}${cell(W.total,tx_(val,{b:1}),{fill:'F5F7FA'})}</w:tr>`;
    tbl+=trow(tx.sub,fmt(t.sub));
    if(q.discount)tbl+=trow(tx.disc,fmt(q.discount));
    if(q.tax)tbl+=trow(tx.tax(q.tax),fmt(t.tax));
    tbl+=trow(tx.grand(cur),fmt(t.total));
  }
  tbl+='</w:tbl>';
  body.push(tbl);

  // الملاحظات
  const lines=termLinesPlain(q);
  if(lines.length){
    body.push(para(run(tx.notes,{b:1,color:'1E3A5F'}),{before:gapTw,after:60}));
    lines.forEach((l,i)=>body.push(para(run((i+1)+'. '+l),{after:Math.round(gapTw*.25)})));
  }
  body.push(para(run(tx.close),{before:lines.length?sigTw:Math.max(sigTw,gapTw)}));
  body.push(para(run(q.preparer||'',{b:1}),{before:gapTw}));

  const sect=`<w:sectPr>${hdrXml?'<w:headerReference w:type="default" r:id="rId2"/>':''}${ftrXml?'<w:footerReference w:type="default" r:id="rId3"/>':''}<w:pgSz w:w="11906" w:h="16838"/><w:pgMar w:top="567" w:right="${sideTw}" w:bottom="567" w:left="${sideTw}" w:header="0" w:footer="0" w:gutter="0"/></w:sectPr>`;
  const docXml=`${XMLH}<w:document ${NS}><w:body>${body.join('')}${sect}</w:body></w:document>`;

  const styles=`${XMLH}<w:styles xmlns:w="http://schemas.openxmlformats.org/wordprocessingml/2006/main"><w:docDefaults><w:rPrDefault><w:rPr><w:rFonts w:ascii="${font}" w:hAnsi="${font}" w:cs="${font}" w:eastAsia="${font}"/><w:sz w:val="${fsHalf}"/><w:szCs w:val="${fsHalf}"/><w:lang w:val="en-US" w:eastAsia="en-US" w:bidi="ar-SA"/></w:rPr></w:rPrDefault><w:pPrDefault><w:pPr><w:spacing w:after="0" w:line="240" w:lineRule="auto"/></w:pPr></w:pPrDefault></w:docDefaults><w:style w:type="paragraph" w:default="1" w:styleId="Normal"><w:name w:val="Normal"/><w:qFormat/></w:style><w:style w:type="table" w:default="1" w:styleId="TableNormal"><w:name w:val="Normal Table"/><w:uiPriority w:val="99"/><w:semiHidden/><w:unhideWhenUsed/><w:tblPr><w:tblInd w:w="0" w:type="dxa"/><w:tblCellMar><w:top w:w="0" w:type="dxa"/><w:left w:w="108" w:type="dxa"/><w:bottom w:w="0" w:type="dxa"/><w:right w:w="108" w:type="dxa"/></w:tblCellMar></w:tblPr></w:style></w:styles>`;

  const relsXml=r=>`${XMLH}<Relationships xmlns="http://schemas.openxmlformats.org/package/2006/relationships">${r.join('')}</Relationships>`;
  const out=[];
  const E=new TextEncoder();
  const add=(name,str)=>out.push({name,data:E.encode(str)});
  add('[Content_Types].xml',`${XMLH}<Types xmlns="http://schemas.openxmlformats.org/package/2006/content-types"><Default Extension="rels" ContentType="application/vnd.openxmlformats-package.relationships+xml"/><Default Extension="xml" ContentType="application/xml"/><Default Extension="png" ContentType="image/png"/><Default Extension="jpeg" ContentType="image/jpeg"/><Override PartName="/word/document.xml" ContentType="application/vnd.openxmlformats-officedocument.wordprocessingml.document.main+xml"/><Override PartName="/word/styles.xml" ContentType="application/vnd.openxmlformats-officedocument.wordprocessingml.styles+xml"/>${hdrXml?'<Override PartName="/word/header1.xml" ContentType="application/vnd.openxmlformats-officedocument.wordprocessingml.header+xml"/>':''}${ftrXml?'<Override PartName="/word/footer1.xml" ContentType="application/vnd.openxmlformats-officedocument.wordprocessingml.footer+xml"/>':''}</Types>`);
  add('_rels/.rels',relsXml([`<Relationship Id="rId1" Type="${REL}/officeDocument" Target="word/document.xml"/>`]));
  add('word/document.xml',docXml);
  add('word/styles.xml',styles);
  const dr=[`<Relationship Id="rId1" Type="${REL}/styles" Target="styles.xml"/>`];
  if(hdrXml)dr.push(`<Relationship Id="rId2" Type="${REL}/header" Target="header1.xml"/>`);
  if(ftrXml)dr.push(`<Relationship Id="rId3" Type="${REL}/footer" Target="footer1.xml"/>`);
  add('word/_rels/document.xml.rels',relsXml(dr.concat(docRels)));
  if(hdrXml){add('word/header1.xml',`${XMLH}<w:hdr ${NS}>${hdrXml}</w:hdr>`);if(hdrRels.length)add('word/_rels/header1.xml.rels',relsXml(hdrRels))}
  if(ftrXml){add('word/footer1.xml',`${XMLH}<w:ftr ${NS}>${ftrXml}</w:ftr>`);if(ftrRels.length)add('word/_rels/footer1.xml.rels',relsXml(ftrRels))}
  return zipStore(out.concat(files));
}
/*DOCX_END*/

const TYPES={price:'عرض سعر',financial:'عرض مالي',technical:'عرض فني'};
const DEF_INTRO={
 ar:{price:'تحية طيبة وبعد ،،،\nيسرنا أن نعرض عليكم الأسعار التالية آملين أن نوفق في خدمتكم',
     financial:'تحية طيبة وبعد ،،،\nيسرنا أن نعرض عليكم العرض المالي التالي آملين أن نوفق في خدمتكم',
     technical:'تحية طيبة وبعد ،،،\nيسرنا أن نعرض عليكم العرض الفني التالي آملين أن نوفق في خدمتكم'},
 en:{price:'Dear Sirs,\nGreetings,\nWe are pleased to submit the following prices, hoping to be of service to you.',
     financial:'Dear Sirs,\nGreetings,\nWe are pleased to submit our financial offer as follows, hoping to be of service to you.',
     technical:'Dear Sirs,\nGreetings,\nWe are pleased to submit our technical offer as follows, hoping to be of service to you.'}
};
const isDefIntro=t=>Object.values(DEF_INTRO).some(o=>Object.values(o).includes(t));
const DEF_FMT={mode:'auto',font:'Tahoma',fs:14,lh:1.7,gap:11,rp:6,sig:28,top:0,side:20};
const FONTS=['Tahoma','Arial','Segoe UI','Calibri','Times New Roman','Traditional Arabic','Simplified Arabic','Sakkal Majalla'];
const LV=[
 {fs:15,lh:2.05,rp:11,gap:22,sig:50},{fs:14.5,lh:1.9,rp:8,gap:16,sig:38},{fs:14,lh:1.7,rp:6,gap:11,sig:28},
 {fs:13,lh:1.55,rp:4,gap:8,sig:20},{fs:12,lh:1.4,rp:2,gap:5,sig:14}
];
const FMT_CTRL=[
 ['fs','حجم الخط',9,20,.5,true],['lh','تباعد الأسطر',1.1,2.4,.05,true],['gap','المسافة بين الفقرات',0,40,1,true],
 ['rp','ارتفاع صفوف الجدول',0,20,1,true],['sig','المسافة قبل التوقيع',0,100,2,true],
 ['top','إزاحة المحتوى للأسفل (ملم)',-8,40,1,false],['side','الهامش الجانبي (ملم)',5,40,1,false]
];
const $=id=>document.getElementById(id);
const esc=s=>String(s??'').replace(/[&<>"']/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]));
const today=()=>new Date().toLocaleDateString('en-CA');
const clone=o=>JSON.parse(JSON.stringify(o));
const mergeFmt=f=>Object.assign({},DEF_FMT,f||{});
let autoLay=LV[2];

function mergeTerms(t){
  const r={};
  TERM_CAT.forEach(c=>{const o=(t&&t[c.k])||{};r[c.k]={on:!!o.on,v:Object.assign({},c.f,o.v||{})}});
  return r;
}
function normalize(q){
  if(typeof q.terms==='string'){q.customTerms=q.terms;q.terms=null}
  q.terms=mergeTerms(q.terms);
  q.customTerms=q.customTerms||'';
  q.items=q.items||[];
  q.items.forEach(i=>{i.spec=i.spec||'';i.img=i.img||'';i.unit=i.unit||''});
  q.showImgs=!!q.showImgs;
  q.lang=q.lang==='en'?'en':'ar';
  q.fileWord=q.fileWord||'';
  q.fmt=mergeFmt(q.fmt);
  delete q.sections;
  return q;
}
function load(){
  let d=null;
  try{d=JSON.parse(localStorage.getItem(KEY))}catch(e){}
  d=d||{};
  d.settings=Object.assign({nextNo:1,letter:'',prepName:'',company:'',companyInfo:'',currency:'دينار أردني',currencyEn:'JOD',decimals:3,tax:0,headerImg:'',footerImg:'',lastTerms:null,lastFmt:null},d.settings||{});
  d.quotes=(d.quotes||[]).map(normalize);
  d.clients=d.clients||[];
  return d;
}
const KEY='quotes_app_v1';
let db=load(), cur;
function persist(){
  try{localStorage.setItem(KEY,JSON.stringify(db));return true}
  catch(e){alert('تعذر الحفظ: مساحة المتصفح ممتلئة (غالباً بسبب الصور). صدّر نسخة احتياطية أو صغّر الصور.');return false}
}
const yy=date=>String((date||today()).slice(2,4));
const makeRef=(date,no)=>`${yy(date)}/${no}/${db.settings.letter||''}`;

function blankQuote(type='price',lang='ar'){
  const s=db.settings;
  return normalize({id:'q'+Date.now(),type,lang,seq:s.nextNo,ref:makeRef(today(),s.nextNo),refAuto:true,
    date:today(),client:'',subject:'',fileWord:'',intro:DEF_INTRO[lang][type],
    items:[{desc:'',spec:'',unit:'',qty:1,price:0,img:''}],showImgs:false,
    tax:s.tax,discount:0,terms:s.lastTerms||{validity:{on:true}},customTerms:'',
    preparer:s.prepName||'',fmt:s.lastFmt,isNew:true,createdAt:Date.now()});
}
function newQuote(){cur=blankQuote();fillForm();$('saveMsg').textContent='';showView('edit')}

/* اسم الملف: رقم-يوم-شهر-العميل-كلمة المحتوى */
function fileBase(q){
  const d=String(q.date||today()).split('-');
  const clean=s=>String(s||'').replace(/[\\/:*?"<>|]/g,'').trim().replace(/\s+/g,'_');
  return [q.seq,d[2],d[1],clean(q.client),clean(q.fileWord)].filter(x=>x!==''&&x!==undefined&&x!==null).join('-');
}
function updFileHint(){$('fileHint').textContent='اسم ملف Word / PDF: '+fileBase(cur)}

/* ---------- صور ---------- */
function readImg(file,maxW,quality,forceJpg,cb){
  const r=new FileReader();
  r.onload=()=>{const im=new Image();im.onload=()=>{
    const sc=Math.min(1,maxW/im.width);
    const c=document.createElement('canvas');c.width=Math.round(im.width*sc);c.height=Math.round(im.height*sc);
    const x=c.getContext('2d');
    const png=!forceJpg&&/png/.test(file.type);
    if(!png){x.fillStyle='#fff';x.fillRect(0,0,c.width,c.height)}
    x.drawImage(im,0,0,c.width,c.height);
    cb(c.toDataURL(png?'image/png':'image/jpeg',quality));
  };im.src=r.result};
  r.readAsDataURL(file);
}
function itemImg(i,inp){
  const f=inp.files[0];if(!f)return;
  readImg(f,500,0.75,true,url=>{cur.items[i].img=url;renderItems();renderPaper()});
}
function delItemImg(i){cur.items[i].img='';renderItems();renderPaper()}
function setHF(k,inp){
  const f=inp.files[0];if(!f)return;
  readImg(f,1600,0.88,false,url=>{db.settings[k]=url;if(persist())fillSettings();renderPaper()});
}
function clearHF(k){db.settings[k]='';persist();fillSettings();renderPaper()}

/* ---------- نموذج ---------- */
function fillForm(){
  document.querySelectorAll('input[name=type]').forEach(r=>r.checked=r.value===cur.type);
  $('ref').value=cur.ref;$('date').value=cur.date;$('client').value=cur.client;$('lang').value=cur.lang;
  $('subject').value=cur.subject;$('fileWord').value=cur.fileWord;$('intro').value=cur.intro;$('customTerms').value=cur.customTerms;
  $('tax').value=cur.tax;$('discount').value=cur.discount;$('preparer').value=cur.preparer;
  $('showImgs').checked=cur.showImgs;
  $('clientsList').innerHTML=db.clients.map(c=>`<option value="${esc(c)}">`).join('');
  applyType();renderItems();renderTerms();syncFmt();updFileHint();renderPaper();
}
function applyType(){
  $('taxRow').style.display=cur.type==='technical'?'none':'flex';
}
document.querySelectorAll('input[name=type]').forEach(r=>r.onchange=()=>{
  cur.type=r.value;
  if(isDefIntro(cur.intro))cur.intro=DEF_INTRO[cur.lang][cur.type];
  $('intro').value=cur.intro;
  applyType();renderItems();renderPaper();
});
$('lang').onchange=()=>{
  cur.lang=$('lang').value;
  if(isDefIntro(cur.intro))cur.intro=DEF_INTRO[cur.lang][cur.type];
  $('intro').value=cur.intro;
  TERM_CAT.forEach(c=>{
    if(!c.fe)return;
    const v=cur.terms[c.k].v;
    for(const n in c.fe){
      if(cur.lang==='en'&&v[n]===c.f[n])v[n]=c.fe[n];
      if(cur.lang==='ar'&&v[n]===c.fe[n])v[n]=c.f[n];
    }
  });
  renderTerms();renderPaper();
};
['ref','date','client','subject','fileWord','intro','customTerms','preparer'].forEach(id=>$(id).oninput=()=>{
  cur[id]=$(id).value;
  if(id==='ref')cur.refAuto=false;
  if(id==='date'&&cur.refAuto&&cur.isNew){cur.ref=makeRef(cur.date,cur.seq);$('ref').value=cur.ref}
  updFileHint();renderPaper();
});
$('tax').oninput=()=>{cur.tax=parseFloat($('tax').value)||0;renderPaper()};
$('discount').oninput=()=>{cur.discount=parseFloat($('discount').value)||0;renderPaper()};
$('showImgs').onchange=()=>{cur.showImgs=$('showImgs').checked;renderItems();renderPaper()};

function renderItems(){
  const tech=cur.type==='technical';
  $('items').innerHTML=cur.items.map((it,i)=>`
   <div class="it">
     <input placeholder="الوصف" value="${esc(it.desc)}" oninput="setItem(${i},'desc',this.value)">
     <textarea placeholder="مواصفات / تفاصيل (اختياري)" oninput="setItem(${i},'spec',this.value)">${esc(it.spec)}</textarea>
     <div class="row">
       <input placeholder="الوحدة" value="${esc(it.unit)}" oninput="setItem(${i},'unit',this.value)">
       <input type="number" step="any" placeholder="الكمية" value="${it.qty}" oninput="setItem(${i},'qty',this.value)">
       ${tech?'':`<input type="number" step="any" placeholder="السعر" value="${it.price}" oninput="setItem(${i},'price',this.value)">`}
       <button class="b red sm" style="flex:0 0 auto" onclick="delItem(${i})">✕</button>
     </div>
     ${cur.showImgs?`<div class="row" style="margin-top:6px">
        <input type="file" accept="image/*" onchange="itemImg(${i},this)">
        ${it.img?`<img class="thumb" src="${it.img}" style="flex:0 0 auto"><button class="b sec sm" style="flex:0 0 auto" onclick="delItemImg(${i})">حذف الصورة</button>`:''}
     </div>`:''}
   </div>`).join('');
}
function setItem(i,k,v){cur.items[i][k]=(k==='qty'||k==='price')?(parseFloat(v)||0):v;renderPaper()}
function addItem(){cur.items.push({desc:'',spec:'',unit:'',qty:1,price:0,img:''});renderItems();renderPaper()}
function delItem(i){cur.items.splice(i,1);renderItems();renderPaper()}

/* ---------- الملاحظات الجاهزة ---------- */
function termHTML(c,st){
  return c.t.replace(/\{(\w+)\}/g,(m,n)=>{
    const num=typeof c.f[n]==='number';
    return `<input class="${num?'ti':'tt'}" type="${num?'number':'text'}" value="${esc(st.v[n])}" oninput="setTV('${c.k}','${n}',this.value)">`;
  });
}
function renderTerms(){
  $('terms').innerHTML=TERM_CAT.map(c=>{
    const st=cur.terms[c.k];
    return `<div class="trm"><input type="checkbox" ${st.on?'checked':''} onchange="togTerm('${c.k}',this.checked)"><span>${termHTML(c,st)}</span></div>`;
  }).join('');
}
function togTerm(k,on){
  cur.terms[k].on=on;
  const c=TERM_CAT.find(x=>x.k===k);
  if(on&&c.ex)cur.terms[c.ex].on=false;
  renderTerms();renderPaper();
}
function setTV(k,n,v){
  const c=TERM_CAT.find(x=>x.k===k);
  cur.terms[k].v[n]=typeof c.f[n]==='number'?(v===''?'':parseFloat(v)):v;
  renderPaper();
}

/* ---------- التنسيق والخطوط ---------- */
$('fmt_font').innerHTML=FONTS.map(f=>`<option>${f}</option>`).join('');
$('fmtRanges').innerHTML=FMT_CTRL.map(([k,l,mn,mx,st])=>
  `<div class="rg"><span>${l}</span><input type="range" id="fmt_${k}" min="${mn}" max="${mx}" step="${st}"><output id="o_${k}"></output></div>`).join('');
function syncFmt(){
  const f=cur.fmt,man=f.mode==='manual';
  document.querySelectorAll('input[name=fmtmode]').forEach(r=>r.checked=r.value===f.mode);
  $('fmt_font').value=f.font;
  FMT_CTRL.forEach(([k,,,,,manualOnly])=>{
    $('fmt_'+k).value=f[k];$('o_'+k).textContent=f[k];
    $('fmt_'+k).disabled=manualOnly&&!man;
  });
}
document.querySelectorAll('input[name=fmtmode]').forEach(r=>r.onchange=()=>{
  if(!r.checked)return;
  if(r.value==='manual'&&cur.fmt.mode!=='manual')Object.assign(cur.fmt,{fs:autoLay.fs,lh:autoLay.lh,gap:autoLay.gap,rp:autoLay.rp,sig:autoLay.sig});
  cur.fmt.mode=r.value;syncFmt();renderPaper();
});
$('fmt_font').onchange=()=>{cur.fmt.font=$('fmt_font').value;renderPaper()};
FMT_CTRL.forEach(([k])=>$('fmt_'+k).oninput=()=>{cur.fmt[k]=parseFloat($('fmt_'+k).value);$('o_'+k).textContent=cur.fmt[k];renderPaper()});
function resetFmt(){cur.fmt=mergeFmt(null);syncFmt();renderPaper()}
function curLayout(){const f=cur.fmt;return f.mode==='manual'?{fs:f.fs,lh:f.lh,gap:f.gap,rp:f.rp,sig:f.sig}:autoLay}
function applyLay(p,L){
  p.style.setProperty('--fs',L.fs+'px');p.style.setProperty('--lh',L.lh);p.style.setProperty('--gap',L.gap+'px');
  p.style.setProperty('--rp',L.rp+'px');p.style.setProperty('--sig',L.sig+'px');
}

/* ---------- المعاينة ---------- */
function renderPaper(){
  const q=cur,s=db.settings,t=totals(q),tech=q.type==='technical',tx=I18N[q.lang],f=q.fmt;
  const en=q.lang==='en';
  const head=s.headerImg?`<img class="hf" src="${s.headerImg}">`:`<div class="co" style="padding:12px ${f.side}mm 8px"><h2>${esc(s.company||'اسم الشركة')}</h2><div>${esc(s.companyInfo)}</div></div>`;
  const foot=s.footerImg?`<img class="hf" src="${s.footerImg}">`:'';
  const introLines=q.intro.split('\n').map(x=>x.trim()).filter(Boolean);
  let h=`<div class="meta"><span>${tx.ref}: <bdi dir="ltr">(${esc(q.ref)})</bdi></span><span>${tx.date}: <bdi dir="ltr">${esc(q.date)}</bdi></span></div>
  <div class="blk addr"><b>${esc(tx.to(q.client))}</b></div>
  ${q.subject?`<div class="blk subj">${tx.subject}: <b>${esc(q.subject)}</b></div>`:''}
  <div class="blk intro">${introLines.map(l=>`<p>${esc(l)}</p>`).join('')}</div>`;

  const img=q.showImgs;
  const cols=1+1+(img?1:0)+1+1+(tech?0:2);
  h+=`<table class="itbl"><tr><th>${tx.no}</th><th>${tx.desc}</th>${img?`<th>${tx.img}</th>`:''}<th>${tx.unit}</th><th>${tx.qty}</th>${tech?'':`<th>${tx.price}</th><th>${tx.total}</th>`}</tr>`+
  q.items.map((it,i)=>`<tr><td>${i+1}</td><td class="l">${esc(it.desc)}${it.spec?`<small>${esc(it.spec)}</small>`:''}</td>${img?`<td>${it.img?`<img src="${it.img}">`:''}</td>`:''}<td>${esc(it.unit)}</td><td>${it.qty}</td>${tech?'':`<td>${fmt(it.price)}</td><td>${fmt(it.qty*it.price)}</td>`}</tr>`).join('');
  if(!tech){
    const curr=en?(s.currencyEn||'JOD'):s.currency;
    h+=`<tr class="tot"><td colspan="${cols-1}">${tx.sub}</td><td>${fmt(t.sub)}</td></tr>`;
    if(q.discount)h+=`<tr class="tot"><td colspan="${cols-1}">${tx.disc}</td><td>${fmt(q.discount)}</td></tr>`;
    if(q.tax)h+=`<tr class="tot"><td colspan="${cols-1}">${esc(tx.tax(q.tax))}</td><td>${fmt(t.tax)}</td></tr>`;
    h+=`<tr class="tot"><td colspan="${cols-1}">${esc(tx.grand(curr))}</td><td>${fmt(t.total)}</td></tr>`;
  }
  h+=`</table>`;

  const lines=termLinesPlain(q);
  if(lines.length)h+=`<h4>${tx.notes}</h4><ol>${lines.map(l=>`<li>${esc(l)}</li>`).join('')}</ol>`;
  h+=`<div class="sig">${tx.close}<br><br><b>${esc(q.preparer)}</b></div>`;

  const p=$('paper');
  p.dir=en?'ltr':'rtl';
  p.innerHTML=`<table class="pg"><thead><tr><td class="hd">${head}</td></tr></thead><tbody><tr><td class="bd" style="padding:${9+f.top}mm ${f.side}mm 7mm"><div class="cnt" style="font-family:'${esc(f.font)}',Tahoma,Arial,sans-serif">${h}</div></td></tr></tbody><tfoot><tr><td class="ft">${foot}</td></tr></tfoot></table>`;
  p.querySelectorAll('img').forEach(im=>{if(!im.complete)im.onload=fit});
  fit();
}

/* ضبط المسافات: تلقائي (أوسع مسافات تناسب صفحة واحدة) أو يدوي */
function fit(){
  const p=$('paper'),cnt=p.querySelector('.cnt');if(!cnt)return;
  p.style.zoom='';
  if(cur.fmt.mode==='manual'){applyLay(p,cur.fmt)}
  else{
    const bd=p.querySelector('td.bd'),cs=getComputedStyle(bd);
    const PAGE=296/25.4*96;
    const avail=PAGE-p.querySelector('thead').offsetHeight-p.querySelector('tfoot').offsetHeight
      -parseFloat(cs.paddingTop)-parseFloat(cs.paddingBottom)-6;
    let pick=-1;
    for(let d=0;d<=4;d++){applyLay(p,LV[d]);if(cnt.offsetHeight<=avail){pick=d;break}}
    if(pick<0){pick=2;applyLay(p,LV[2])}
    autoLay=LV[pick];
  }
  const w=p.parentElement.clientWidth,pw=210/25.4*96;
  if(w&&w<pw)p.style.zoom=(w/pw).toFixed(3);
}
window.addEventListener('resize',fit);
if(document.fonts&&document.fonts.ready)document.fonts.ready.then(fit);

/* اسم الملف عند حفظ PDF من نافذة الطباعة */
let _title=document.title;
window.addEventListener('beforeprint',()=>{_title=document.title;if(cur)document.title=fileBase(cur)});
window.addEventListener('afterprint',()=>{document.title=_title});

function exportWord(){
  fit();
  const blob=buildDocx(cur,db.settings,curLayout(),I18N[cur.lang]);
  const a=document.createElement('a');
  a.href=URL.createObjectURL(blob);a.download=fileBase(cur)+'.docx';
  document.body.appendChild(a);a.click();a.remove();
  setTimeout(()=>URL.revokeObjectURL(a.href),4000);
}

/* ---------- حفظ وقائمة ---------- */
function saveQuote(){
  if(!cur.client.trim()){alert('اكتب اسم العميل أولاً');$('client').focus();return false}
  const c=cur.client.trim();
  if(!db.clients.includes(c))db.clients.push(c);
  const i=db.quotes.findIndex(x=>x.id===cur.id);
  const copy=clone(cur);copy.isNew=false;copy.total=totals(cur).total;
  const wasNew=i<0;
  if(i>=0)db.quotes[i]=copy;
  else{
    db.quotes.push(copy);
    if(cur.seq===db.settings.nextNo)db.settings.nextNo++;
  }
  db.settings.lastTerms=clone(cur.terms);
  db.settings.lastFmt=clone(cur.fmt);
  if(!persist()){
    if(wasNew){db.quotes.pop();db.settings.nextNo=cur.seq}
    return false;
  }
  cur.isNew=false;
  $('clientsList').innerHTML=db.clients.map(c=>`<option value="${esc(c)}">`).join('');
  $('saveMsg').textContent='✔ تم الحفظ — الرقم التالي: '+makeRef(today(),db.settings.nextNo);
  return true;
}
function convertTo(){
  const t=$('convType').value;
  if(t===cur.type){alert('اختر نوعاً مختلفاً عن النوع الحالي');return}
  if(!saveQuote())return;
  const o=clone(cur),n=blankQuote(t,o.lang);
  Object.assign(n,{client:o.client,subject:o.subject,fileWord:o.fileWord,items:o.items,showImgs:o.showImgs,tax:o.tax,discount:o.discount,terms:o.terms,customTerms:o.customTerms,preparer:o.preparer,fmt:o.fmt});
  cur=n;fillForm();
  $('saveMsg').textContent='تم إنشاء '+TYPES[t]+' جديد بنفس المعلومات برقم '+cur.ref+' (لم يُحفظ بعد).';
}
function renderList(){
  const q=$('q').value.trim().toLowerCase();
  const rows=[...db.quotes].sort((a,b)=>b.createdAt-a.createdAt).filter(x=>!q||(x.client+x.ref+x.subject).toLowerCase().includes(q));
  $('listBody').innerHTML=rows.map(x=>`<tr>
    <td dir="ltr" style="text-align:right">${esc(x.ref)}</td><td>${esc(x.date)}</td><td>${esc(x.client)}</td>
    <td>${TYPES[x.type]}${x.lang==='en'?' (EN)':''}</td><td>${x.type==='technical'?'—':fmt(x.total||0)}</td>
    <td class="actions"><button class="b sm" onclick="openQ('${x.id}')">فتح / تعديل</button>
    <button class="b sec sm" onclick="dupQ('${x.id}')">نسخ</button>
    <button class="b red sm" onclick="delQ('${x.id}')">حذف</button></td></tr>`).join('');
  $('emptyMsg').textContent=rows.length?'':'لا توجد عروض محفوظة.';
}
$('q').oninput=renderList;
function openQ(id){cur=normalize(clone(db.quotes.find(x=>x.id===id)));cur.isNew=false;fillForm();$('saveMsg').textContent='';showView('edit')}
function dupQ(id){
  cur=normalize(clone(db.quotes.find(x=>x.id===id)));
  cur.id='q'+Date.now();cur.seq=db.settings.nextNo;cur.date=today();cur.ref=makeRef(cur.date,cur.seq);
  cur.refAuto=true;cur.isNew=true;cur.createdAt=Date.now();
  fillForm();showView('edit');
}
function delQ(id){
  const o=db.quotes.find(x=>x.id===id);
  if(!confirm('حذف العرض '+o.ref+' للعميل '+o.client+'؟'))return;
  db.quotes=db.quotes.filter(x=>x.id!==id);persist();renderList();
}

/* ---------- إعدادات ---------- */
function fillSettings(){
  const s=db.settings;
  $('s_next').value=s.nextNo;$('s_letter').value=s.letter;$('s_prep').value=s.prepName;
  $('s_co').value=s.company;$('s_coinfo').value=s.companyInfo;
  $('s_cur').value=s.currency;$('s_curen').value=s.currencyEn;$('s_dec').value=s.decimals;$('s_tax').value=s.tax;
  [['p_head','headerImg'],['p_foot','footerImg']].forEach(([id,k])=>{
    const im=$(id);im.style.display=s[k]?'block':'none';im.src=s[k]||'';
  });
}
function saveSettings(){
  const s=db.settings;
  s.nextNo=Math.max(1,parseInt($('s_next').value)||1);s.letter=$('s_letter').value.trim();
  s.prepName=$('s_prep').value;
  s.company=$('s_co').value;s.companyInfo=$('s_coinfo').value;s.currency=$('s_cur').value;s.currencyEn=$('s_curen').value||'JOD';
  s.decimals=Math.min(3,Math.max(0,parseInt($('s_dec').value)||0));s.tax=parseFloat($('s_tax').value)||0;
  persist();
  if(cur.isNew&&cur.refAuto){cur.seq=s.nextNo;cur.ref=makeRef(cur.date,cur.seq);cur.tax=s.tax;if(!cur.preparer)cur.preparer=s.prepName}
  fillForm();
  alert('تم حفظ الإعدادات');
}
function exportData(){
  const a=document.createElement('a');
  a.href=URL.createObjectURL(new Blob([JSON.stringify(db)],{type:'application/json'}));
  a.download='quotes-backup-'+today()+'.json';a.click();
}
function importData(e){
  const f=e.target.files[0];if(!f)return;
  const r=new FileReader();
  r.onload=()=>{try{
    const d=JSON.parse(r.result);
    if(!d.quotes||!d.settings)throw 0;
    if(!confirm('سيتم استبدال كل البيانات الحالية. متابعة؟'))return;
    localStorage.setItem(KEY,JSON.stringify(d));db=load();newQuote();fillSettings();alert('تم الاستيراد');
  }catch(x){alert('ملف غير صالح')}};
  r.readAsText(f);
}

/* ---------- تنقل ---------- */
function showView(v){
  document.querySelectorAll('.view').forEach(e=>e.classList.toggle('on',e.id==='v-'+v));
  document.querySelectorAll('.tab').forEach(e=>e.classList.toggle('on',e.dataset.v===v));
  if(v==='edit')fit();
  if(v==='list')renderList();
  if(v==='set')fillSettings();
}
document.querySelectorAll('.tab').forEach(b=>b.onclick=()=>showView(b.dataset.v));

cur=blankQuote();fillForm();
if(!db.settings.letter)showView('set');
</script>
</body>
</html>
