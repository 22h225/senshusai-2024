<script lang="ts">
	import { onMount } from 'svelte';
	import { course, comparison } from './constants'

	import floor1 from '$lib/assets/1F.png';
	import floor2 from '$lib/assets/2F.png';
	import floor3 from '$lib/assets/3F.png';

	class Node {
		id: number;
		edgesTo: Node[];
		edgesCost: number[];
		done: boolean;
		cost: number;
		previousNode: Node | null;

		constructor(id: number) {
			this.edgesTo = [];
			this.edgesCost = [];
			this.done = false;
			this.cost = -1;
			this.id = id;
			this.previousNode = null;
		}

		addNode(node: Node, cost: number) {
			this.edgesTo.push(node);
			this.edgesCost.push(cost);
		}
	}

let coordinates = [
    //0 入口
    [
        [1.61,0.74]
    ],
    //1 3-A
    [
        [2.29,0.6]
    ],
    //2 3-B
    [
        [2.19,0.6]
    ],
    //3 3-C
    [
        [2.09,0.6]
    ],
    //4 3-D
    [
        [1.99,0.6]
    ],
    //5 3-E
    [
        [1.71,0.6]
    ],
    //6 3-F
    [
        [1.61,0.6]
    ],
    //7 3-G
    [
        [1.51,0.6]
    ],
    //8 3-H
    [
        [1.41,0.6]
    ],
    //9 化学部
    [
        [2.14,0.26]
    ],
    //10 教務部総合担当
    [
        [1.96,0.26]
    ],
    //11 2-G
    [
        [1.71,0.26]
    ],
    //12 2-C
    [
        [1.61,0.26]
    ],
    //13 写真部
    [
        [1.84,0.38]
    ],
    //14 工芸部
    [
        [1.49,0.97]
    ],
    //15 オーケストラ部
    [
        [1.23,0.73]
    ],
    //16 ダンス部
    [
        [1.23,0.73]
    ],
    //17 空手拳法玄気道部
    [
        [1.23,0.83]
    ],
    //18 山岳部
    [
        [2.02,1.39]
    ],
    //19 高校演劇部
    [
        [1.69,1.29]
    ],
    //20 中学演劇部
    [
        [1.69,1.29]
    ],
    //21 合唱部
    [
        [1.69,1.29]
    ],
    //22 クラシックギター部
    [
        [1.69,1.29]
    ],
    //23 千葉高ピアノの会
    [
        [1.69,1.29]
    ],
    //24 Lightbious
    [
        [1.69,1.29]
    ],
    //25 地理部(渡り廊下)
    [
        [1.9,1.94]
    ],
    //26 弓道部
    [
        [2.51,0.26]
    ],
    //27 華道部
    [
        [2.51,0.6]
    ],
    //2Fはy座標+1.46 (-1.24)
    //28 2-A
    [
        [2.31,2.16]
    ],
    //29 2-B
    [
        [2.21,2.16]
    ],
    //30 2-H
    [
        [2.11,2.16]
    ],
    //31 2-D
    [
        [2.01,2.16]
    ],
    //32 2-E
    [
        [1.78,2.16]
    ],
    //33 2-F
    [
        [1.68,2.16]
    ],
    //34 文実執行部
    [
        [1.58,2.16]
    ],
    //35 将棋部
    [
        [1.48,2.16]
    ],
    //36 囲碁部
    [
        [1.48,2.16]
    ],
    //37 数楽研究会
    [
        [1.9,1.94]
    ],
    //38 競技かるた同好会
    [
        [1.75,2.62]
    ],
    //39 GSU
    [
        [2.18,1.86]  
    ],
    //3Fは+2.92 (-2.48)
    //40 1-A
    [
        [2.22,3.58]
    ],
    //41 1-B
    [
        [2.12,3.58]
    ],
    //42 1-C
    [
        [2.01,3.58]
    ],
    //43 1-D
    [
        [1.89,3.58]
    ],
    //44 1-E
    [
        [1.55,3.58]
    ],
    //45 1-F
    [
        [1.44,3.58]
    ],
    //46 1-G
    [
        [1.32,3.58]
    ],
    //47 1-H
    [
        [1.21,3.58]
    ],
    //48 漫画研究部
    [
        [1.65,3.66]
    ],
    //49 生物研究部
    [
        [2.05,3.17]
    ],
    //50 クイズ研究部
    [
        [1.53,3.17]
    ],
    //51 文学部
    [
        [1.38,3.17]
    ],
    //52 鉄道研究部
    [
        [0.83,3.22]
    ],
    //53 美術部 
    [
        [1.98,4.17]
    ],
    //54 茶道部
    [
        [1.51,4.17]
    ],
    //55 書道部
    [
        [1.23,0.73]
    ],
    //56 フォークソング部
    [
        [0.76,4.07]
    ],
    //57 1-1
    [
        [0.56,2.1]
    ],
    //58 1-2
    [
        [0.49,2.1]
    ],
    //59 2-1
    [
        [0.34,2.04]
    ],
    //60 2-2
    [
        [0.34,2.25]
    ],
    //61 3-1
    [
        [0.34,2.35]
    ],
    //62 3-2
    [
        [0.34,2.45]
    ],
    //63 中学生徒会
    [
        [0.54,0.59]
    ],
    //64 中学学習委員会
    [
        [0.54,0.59]
    ],
    //65 中学図書委員会
    [
        [0.54,0.59]
    ],
    //66 中学書道部
    [
        [0.54,0.59]
    ],
    //67 1F中央infodesk
    [
        [1.82,0.66]
    ],
    //68 2F中央
    [
        [1.89,2.19]
    ],
    //69 3F中央
    [
        [1.7,3.52]
    ],
    //70 1F右側
    [
        [2.39,0.6]
    ],
    //71 2F右側
    [
        [2.39,2.16]
    ],
    //72 3F右側
    [
        [2.34,3.57]
    ],
    //73 1F左側
    [
        [1.32,0.6]
    ],
    //74 2F左側
    [
        [1.42,2.16]
    ],
    //75 3F左側
    [
        [1.1,3.57]
    ],
    //76 理科棟1F
    [
        [1.84,0.26]
    ],
    //77 理科棟2F
    [
        [1.91,1.86]
    ],
    //78 理科棟3F
    [
        [1.71,3.17]
    ],
    //79 社会科1F
    [
        [1.15,0.3]
    ],
    //80 社会科2F
    [
        [1.28,1.89]
    ],
    //81 社会科3F
    [
        [0.91,3.22]
    ],
    //82 管理1F
    [
        [1.9,1.1]
    ],
    //83 管理2F
    [
        [1.96,2.63]
    ],
    //84 管理3F
    [
        [1.78,4.18]
    ],
    //85 小体育館前
    [
        [0.99,0.92]
    ],
    //86 社会科前
    [
        [1.01,0.33]
    ],
    //87 中学外
    [
        [0.65,0.92]
    ],
    //88 中学入り口
    [
        [0.65,0.52]
    ],
    //89 中学出口1F 
    [
        [0.35,0.92]
    ],
    //90 中学1F
    [
        [0.57,0.54]
    ],
    //91 中学2F
    [
        [0.39,2.12]
    ],
    //92 中学出口2F
    [
        [0.34,2.61]
    ],
    //93 HR1FWC
    [
        [1.87,0.66]
    ],
    //94 HR2FWC
    [
        [1.92,2.22]
    ],
    //95 HR3FWC
    [
        [1.74,3.66]
    ],
    //96 理科1FWC
    [
        [1.81,0.2]
    ],
    //97 理科2FWC
    [
        [1.85,1.85]
    ],
    //98 理科3FWC
    [
        [1.63,3.18]
    ],
    //99 管理1FWC
    [
        [1.85,1.11]
    ],
    //100 管理2FWC
    [
        [1.9,1.63]
    ],
    //101 管理3FWC
    [
        [1.71,4.2]
    ],
    //102 社会1FWC
    [
        [1.16,0.31]
    ],
    //103 社会2FWC
    [
        [1.27,1.9]
    ],
    //104 中学1FWC
    [
        [0.36,0.56]
    ],
    //105 中学2FWC
    [
        [0.34,2.14] 
    ],
    //106 地理部（講堂前）
    [
        [1.74,1.46]
    ],
    //107 書道部（書道室）
    [
        [1.25,4.17]
    ],
    //108 大会議室
    [
        [1.63,2.6]
    ],
    //109 教務室
    [
        [2.03,2.6]
    ],
    //110 コンピュータ研究部
    [
        [1.1,3.17]
    ],
    //111 中学棟北側
    [
        [0.67,0.4]
    ],
    //112 体育館前
    [
        [1.23,0.74]
    ]
]


//numberかnumber[]が含まれる配列
function multiplyArray(arr: any[]): any[] {
    return arr.map(item => {
        if (Array.isArray(item)) {
            return multiplyArray(item); // 再帰的に処理する
        } else {
            return item * 128; // ピクセル変換
        }
    });
}
coordinates = multiplyArray(coordinates);

let canvas: HTMLCanvasElement | null;
let time: HTMLElement | null;
let s_select: HTMLSelectElement;
let g_select: HTMLSelectElement;
let button: HTMLButtonElement;

function main(s:number ,g:number){
    //ノード数
    let N = 113
    let nodes = []
    //スタートノード
    let start = s
    //ゴールノード
    let goal = g
    for (let i = 0; i < N; i++) {
      //ノードiの定義
      nodes[i] = new Node(i)
    }
  
    //ノードiについて
    for (let i = 0; i < N; i++) {
      for(let j = 0; j < course[i].length; j++){
        //course[i][j][0]はゴールノード course[i][j][1]はコスト 
        nodes[i].addNode(nodes[course[i][j][0]], course[i][j][1])
      }
    }
  
    // スタートノードのコストを0に設定
    nodes[start].cost = 0
  
    // Dijkstraのメインループ
    while (true) {
      let processNode = null;
  
      for (let i = 0; i < nodes.length; i++) {
        let node = nodes[i];
  
        if (node.done || node.cost < 0) continue;
  
        if (!processNode || node.cost < processNode.cost) {
          processNode = node;
        }
      }
      if (!processNode) {
        break;
      }
  
      processNode.done = true;
  
      for (let i = 0; i < processNode.edgesTo.length; i++) {
        let node = processNode.edgesTo[i];
        let cost = processNode.cost + processNode.edgesCost[i];
        let needsUpdate = (node.cost < 0) || (node.cost > cost);
        if (needsUpdate) {
          node.cost = cost;
          node.previousNode = processNode; // 前のノードを記録
        }
      }
    }
  
    // ゴールノードまでの最短コストを出力
    //1コスト6秒
    console.log(nodes[goal].cost * 6);
  
    // キャンバスとそのコンテキストを取得
// const canvas = document.getElementById('canvas') as HTMLCanvasElement | null;
let ctx:any
if (canvas) {
    ctx = canvas.getContext('2d');
    // ctxの使用処理
} else {
    console.error("Canvas element not found");
}

    // 描画する線を設定
    ctx.strokeStyle = 'red'; // 線の色
    ctx.lineWidth = 2; // 線の太さ
	if (canvas) {
		ctx.clearRect(0, 0, canvas.width, canvas.height)
		// ctxの使用処理
	} else {
		console.error("Canvas element not found");
	}
    // 線の情報を配列として持つ
    const lines = [];


    // 経路を復元して出力
    let path = [];
    let currentNode:Node|null = nodes[goal]; // ゴールノードからスタート
    // 前のノードをたどっていく
    while (currentNode) {
      path.push(currentNode.id); 
      let currentId = currentNode.id
      currentNode = currentNode.previousNode;
      if(currentNode !== null){
        let nodeId = currentNode.id
        //x1 ->x2逆順
        let line = { x1: coordinates[currentId][0][0], y1: coordinates[currentId][0][1],
          x2: coordinates[nodeId][0][0], y2: coordinates[nodeId][0][1] }
        lines.push(line)  
      }
    }
        
    // 配列の各線について描画
    lines.forEach(line => {
        drawLine(line.x1, line.y1, line.x2, line.y2);

        // 各頂点に円を描く
        drawCircle(line.x1, line.y1);  // 始点に円を描画
        drawCircle(line.x2, line.y2);  // 終点に円を描画
    });
    
    function drawLine(x1:number, y1:number, x2:number, y2:number) {
        ctx.beginPath();
        ctx.moveTo(x1, y1);
        ctx.lineTo(x2, y2);
        ctx.stroke();
    }

    function drawCircle(x:number, y:number) {
        ctx.beginPath();
        ctx.arc(x, y, 5, 0, 2 * Math.PI);  // 半径5の円を描く
        ctx.fillStyle = 'red';  // 円の色
        ctx.fill();  // 塗りつぶし
    }

    // 経路を逆順にして表示
    console.log(path.reverse().join(" -> "));


    //時間の表示
	// const time = document.getElementById("target_time") as HTMLElement | null;
	if (time) {
		time.textContent = Math.round(nodes[goal].cost / 10).toString();
	}
}

// window.onload = () => main(0, 110);

onMount(() => {
	main(0, 110)

// button.addEventListener("click", function() {
//     const value1 = parseInt(s_select.value, 10); // 10進数として変換
//     const value2 = parseInt(g_select.value, 10); // 10進数として変換
//     main(value1, value2);}, false);
});

function buttonOnClick() {
    const value1 = parseInt(s_select.value, 10); // 10進数として変換
    const value2 = parseInt(g_select.value, 10); // 10進数として変換
    main(value1, value2);
};

// const s_select = document.getElementById("s_select") as HTMLButtonElement
// const g_select = document.getElementById("g_select") as HTMLButtonElement
// const button = document.getElementById("submit") as HTMLButtonElement
</script>

<div class="container h-full mx-auto flex justify-center pt-8">
	<div class="space-y-10 text-center flex flex-col items-center">
		<h2 class="h2">経路検索</h2>
	</div>
	<div id="select">
        <div>
            <label for="s_select"><span class="label">出発地</span></label>
            <select name="start" id="s_select" bind:this={s_select} placeholder="出発地">
                <option value="0">入口</option>
                <option value="1">3-A</option>
                <option value="2">3-B</option>
                <option value="3">3-C</option>
                <option value="4">3-D</option>
                <option value="5">3-E</option>
                <option value="6">3-F</option>
                <option value="7">3-G</option>
                <option value="8">3-H</option>
                <option value="9">化学部</option>
                <option value="10">教務部総合担当</option>
                <option value="11">2-G</option>
                <option value="12">2-C</option>
                <option value="13">写真部</option>
                <option value="14">工芸部</option>
                <option value="15">オーケストラ部</option>
                <option value="16">ダンス部</option>
                <option value="17">空手拳法玄気道部</option>
                <option value="18">山岳部</option>
                <option value="19">高校演劇部</option>
                <option value="20">中学演劇部</option>
                <option value="21">合唱部</option>
                <option value="22">クラシックギター部</option>
                <option value="23">千葉高ピアノの会</option>
                <option value="24">Lightbious</option>
                <option value="25">地理部(渡り廊下)</option>
                <option value="26">弓道部</option>
                <option value="27">華道部</option>
                <option value="28">2-A</option>
                <option value="29">2-B</option>
                <option value="30">2-H</option>
                <option value="31">2-D</option>
                <option value="32">2-E</option>
                <option value="33">2-F</option>
                <option value="34">文実執行部</option>
                <option value="35">将棋部</option>
                <option value="36">囲碁部</option>
                <option value="37">数楽研究会</option>
                <option value="38">競技かるた同好会</option>
                <option value="39">グローバルサイエンス部</option>
                <option value="40">1-A</option>
                <option value="41">1-B</option>
                <option value="42">1-C</option>
                <option value="43">1-D</option>
                <option value="44">1-E</option>
                <option value="45">1-F</option>
                <option value="46">1-G</option>
                <option value="47">1-H</option>
                <option value="48">漫画研究部</option>
                <option value="49">生物研究部</option>
                <option value="50">クイズ研究部</option>
                <option value="51">文学部</option>
                <option value="52">鉄道研究部</option>
                <option value="53">美術部</option>
                <option value="54">茶道部</option>
                <option value="55">書道部</option>
                <option value="56">フォークソング部</option>
                <option value="57">1-1</option>
                <option value="58">1-2</option>
                <option value="59">2-1</option>
                <option value="60">2-2</option>
                <option value="61">3-1</option>
                <option value="62">3-2</option>
                <option value="63">中学生徒会</option>
                <option value="64">中学学習委員会</option>
                <option value="65">中学図書委員会</option>
                <option value="66">中学書道部</option>
                <option value="67">1F中央階段(infodesk)</option>
                <option value="68">2F中央階段</option>
                <option value="69">3F中央階段</option>
                <option value="70">1F西階段</option>
                <option value="71">2F西階段</option>
                <option value="72">3F西階段</option>
                <option value="73">1F東階段</option>
                <option value="74">2F東階段</option>
                <option value="75">3F東階段</option>
                <option value="76">理科棟1F階段</option>
                <option value="77">理科棟2F階段</option>
                <option value="78">理科棟3F階段</option>
                <option value="79">社会科棟1F階段</option>
                <option value="80">社会科棟2F階段</option>
                <option value="81">社会科棟3F階段</option>
                <option value="82">管理棟1F階段</option>
                <option value="83">管理棟2F階段</option>
                <option value="84">管理棟3F階段</option>
                <option value="85">小体育館前</option>
                <option value="86">社会科棟前</option>
                <option value="87">中学棟前</option>
                <option value="88">中学棟入口</option>
                <option value="89">中学1F外階段</option>
                <option value="90">中学1F中階段</option>
                <option value="91">中学2F中階段</option>
                <option value="92">中学2F外階段</option>
                <option value="93">1Fトイレ</option>
                <option value="94">2Fトイレ</option>
                <option value="95">3Fトイレ</option>
                <option value="96">理科棟1Fトイレ</option>
                <option value="97">理科棟2Fトイレ</option>
                <option value="98">理科棟3Fトイレ</option>
                <option value="99">管理棟1Fトイレ</option>
                <option value="100">管理棟2Fトイレ</option>
                <option value="101">管理棟3Fトイレ</option>
                <option value="102">社会科棟1Fトイレ</option>
                <option value="103">社会科棟2Fトイレ</option>
                <option value="104">中学棟1Fトイレ</option>
                <option value="105">中学棟2Fトイレ</option>
                <option value="106">地理部(講堂前)</option>
                <option value="107">書道部(書道室)</option>
                <option value="108">大会議室</option>
                <option value="109">教務室</option>
                <option value="110">コンピュータ―研究部<option value="">
            </select>    
        </div>
        <div>
            <label for="g_select"><span class="label">目的地</span></label>
            <select name="goal" id="g_select" bind:this={g_select}>
                <option value="0">入口</option>
                <option value="1">3-A</option>
                <option value="2">3-B</option>
                <option value="3">3-C</option>
                <option value="4">3-D</option>
                <option value="5">3-E</option>
                <option value="6">3-F</option>
                <option value="7">3-G</option>
                <option value="8">3-H</option>
                <option value="9">化学部</option>
                <option value="10">教務部総合担当</option>
                <option value="11">2-G</option>
                <option value="12">2-C</option>
                <option value="13">写真部</option>
                <option value="14">工芸部</option>
                <option value="15">オーケストラ部</option>
                <option value="16">ダンス部</option>
                <option value="17">空手拳法玄気道部</option>
                <option value="18">山岳部</option>
                <option value="19">高校演劇部</option>
                <option value="20">中学演劇部</option>
                <option value="21">合唱部</option>
                <option value="22">クラシックギター部</option>
                <option value="23">千葉高ピアノの会</option>
                <option value="24">Lightbious</option>
                <option value="25">地理部(渡り廊下)</option>
                <option value="26">弓道部</option>
                <option value="27">華道部</option>
                <option value="28">2-A</option>
                <option value="29">2-B</option>
                <option value="30">2-H</option>
                <option value="31">2-D</option>
                <option value="32">2-E</option>
                <option value="33">2-F</option>
                <option value="34">文実執行部</option>
                <option value="35">将棋部</option>
                <option value="36">囲碁部</option>
                <option value="37">数楽研究会</option>
                <option value="38">競技かるた同好会</option>
                <option value="39">グローバルサイエンス部</option>
                <option value="40">1-A</option>
                <option value="41">1-B</option>
                <option value="42">1-C</option>
                <option value="43">1-D</option>
                <option value="44">1-E</option>
                <option value="45">1-F</option>
                <option value="46">1-G</option>
                <option value="47">1-H</option>
                <option value="48">漫画研究部</option>
                <option value="49">生物研究部</option>
                <option value="50">クイズ研究部</option>
                <option value="51">文学部</option>
                <option value="52">鉄道研究部</option>
                <option value="53">美術部</option>
                <option value="54">茶道部</option>
                <option value="55">書道部</option>
                <option value="56">フォークソング部</option>
                <option value="57">1-1</option>
                <option value="58">1-2</option>
                <option value="59">2-1</option>
                <option value="60">2-2</option>
                <option value="61">3-1</option>
                <option value="62">3-2</option>
                <option value="63">中学生徒会</option>
                <option value="64">中学学習委員会</option>
                <option value="65">中学図書委員会</option>
                <option value="66">中学書道部</option>
                <option value="67">1F中央階段(infodesk)</option>
                <option value="68">2F中央階段</option>
                <option value="69">3F中央階段</option>
                <option value="70">1F西階段</option>
                <option value="71">2F西階段</option>
                <option value="72">3F西階段</option>
                <option value="73">1F東階段</option>
                <option value="74">2F東階段</option>
                <option value="75">3F東階段</option>
                <option value="76">理科棟1F階段</option>
                <option value="77">理科棟2F階段</option>
                <option value="78">理科棟3F階段</option>
                <option value="79">社会科棟1F階段</option>
                <option value="80">社会科棟2F階段</option>
                <option value="81">社会科棟3F階段</option>
                <option value="82">管理棟1F階段</option>
                <option value="83">管理棟2F階段</option>
                <option value="84">管理棟3F階段</option>
                <option value="85">小体育館前</option>
                <option value="86">社会科棟前</option>
                <option value="87">中学棟前</option>
                <option value="88">中学棟入口</option>
                <option value="89">中学1F外階段</option>
                <option value="90">中学1F中階段</option>
                <option value="91">中学2F中階段</option>
                <option value="92">中学2F外階段</option>
                <option value="93">1Fトイレ</option>
                <option value="94">2Fトイレ</option>
                <option value="95">3Fトイレ</option>
                <option value="96">理科棟1Fトイレ</option>
                <option value="97">理科棟2Fトイレ</option>
                <option value="98">理科棟3Fトイレ</option>
                <option value="99">管理棟1Fトイレ</option>
                <option value="100">管理棟2Fトイレ</option>
                <option value="101">管理棟3Fトイレ</option>
                <option value="102">社会科棟1Fトイレ</option>
                <option value="103">社会科棟2Fトイレ</option>
                <option value="104">中学棟1Fトイレ</option>
                <option value="105">中学棟2Fトイレ</option>
                <option value="106">地理部(講堂前)</option>
                <option value="107">書道部(書道室)</option>
                <option value="108">大会議室</option>
                <option value="109">教務室</option>
                <option value="110" selected>コンピュータ―研究部<option value="">
            </select>
            <div id="sub_parent">
                <button id="submit" bind:this={button} on:click={buttonOnClick}>検索</button>
            </div>
    
        </div>
    </div>
    <div id="main">
        <div class="floor_container">
            <img src={floor1} alt="1階"> 
            <img src={floor2} alt="2階"> 
            <img src={floor3} alt="3階"> 
            <canvas id="canvas" bind:this={canvas} width="350" height="570"></canvas>
        </div>
        <div id="sub">
            <div id="time">
                <p style="margin: 1em 0 1em 0;">かかる時間</p>
                <p>約<span id="target_time" bind:this={time}></span>分</p>
            </div>
        </div>
    </div>
    <div id="route">
    </div>

</div>
<style lang="postcss">
	
.container{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
}

.floor_container {
    position: relative;
    width: 350px; /* 画像とキャンバスの幅 */
    height: 570px; /* 画像とキャンバスの高さ */
    margin-right:90px;
}

img {
    width: 350px;
    height: auto;
    display: block;
}

img[alt="2階"]{
    border-top : 5px black dashed;
    border-bottom : 5px black dashed;
}
canvas {
    position: absolute;
    top: 0;
    left: 0;
    z-index: 10; /* キャンバスを画像の上に表示する */
}

select {
    width: 250px;
    border: 2px solid #007bff;
    border-radius: 6px;
    padding: 10px;
    font-size: 16px;
    background-color: #fff;
    color: #333;
    outline: none;
}
select:focus {
    border-color: #0056b3;
    box-shadow: 0 0 0 0.2rem rgba(38, 143, 255, 0.25);
}
.label{
    border-radius: 10px;
    background: #0079fa;
    color: white;
    margin: 10px;
    padding: 5px;
}

#select{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 1ch;
}

#sub_parent{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 1ch;
    width: 350px;
}

#submit{
    border-radius: 100px;
    background: #0079fa;
    color: white;
    padding: 5px;
}

#submit:hover{
    background: #8ac3ff;
    transition: .5s;
    cursor: pointer;
}
#main{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 1ch;
}

#time{
    display: flex;
    flex-direction: column;
}

#sub{
    width: calc(100vw - 460px);
}

p{
    margin: 0;
}

#target_time{
    font-size: 80px;
}
</style>
