---
title: Sudoku
author: Vivian.Balakrishnan
layout: page
order: 50
---



*	Sudoku Solver translated into Javascript from [original code in C++](https://drive.google.com/drive/folders/0B2G2LjIu7WbdfjhaUmVzc1lCR2hUdk5fZllCOHdtbFItbU5qYzdqZGVxdmlnRkJyYVQ4VU0)
*		by Lee Hsien Loong
*	The MIT License (MIT)
*	Copyright (c) 2015 Vivian Balakrishnan



<style>
    p { text-align: left; }
    table { border: 2px solid #000; border-collapse: collapse;
            margin-left: auto; margin-right: auto; }
    input { border: 2px solid #ccc; }
</style>

<script type="text/javascript">


  BOARD_SIZE = 9;         // Width and height of the SuDoku board
	BOX_SIZE = 3;           // Width and height of the inner boxes
	EMPTY = "";             // Empty cell marker
	BLANK = 0x0;
	ONES = 0x3fe;			//	Binary 1111111110
	var InBlock = [];
	var InRow = [];
	var InCol = [];
	var board = [];			// Board of 81 cells

	var Block = [];			// 3x3 block of cells
	var Row = [];			// Row of 9 cells
	var Col = [];			// Column of 9 cells
	var Seq = []; 			// Sequence of blank cells
	var SeqPos = 0; 		// Points to blank cells



    function nextfield(me){
    	var vnum=/[1-9]/;
        var elements=document.getElementsByTagName("input");
			for (i=0; i<elements.length; i++) {

				if (elements[i]==me) {
					break;
					}
			}
		if (!elements[i].value.match(vnum)) {  

					elements[i].value="";
					elements[i].focus();
		}	else	{
        elements[i+1].focus();

        }
    }


    function draw() {
    	document.write('<table style="float:center">');
    	for (var row=0; row<9; row++) {
    		document.write('<tr>');
    		for (var col=0; col<9; col++) {
				document.write('<td><input type="text" size="2" maxlength="1" style="font-size:20px" onkeyup="nextfield(this)"/></td>');
			}
			document.write('</tr>');
    	}
    	document.write('</table>');
    }


	function setup() {
			board = document.getElementsByTagName("input");
     		for (var i=0; i<81; i++) {
     			var Square = i;
     			InRow[Square] = (Math.floor(Square / BOARD_SIZE));
     			InCol[Square] = (Square % BOARD_SIZE);
     			InBlock[Square] = ((Math.floor(Square/27) ) * 3)  + (Math.floor((Square % BOARD_SIZE) / 3));	  		
     		}	   

            for (var i=0; i<9; i++) {
            	Block[i] = ONES;
            	Row[i] = ONES;
            	Col[i] = ONES;
		  	}

		}

	function bitcount(b){
		b=b>>>1;
		var count = 0;
		while (b) {
			b= (b >>> 1);
			count++;
		}
		return count;
	}

	function removeValbit(c,v) {
		Block[InBlock[c]] &= ~v;
		Row[InRow[c]] &= ~v;
		Col[InCol[c]] &= ~v;
	}

	function test(SeqNum) {

		if (SeqNum>=Seq.length) return true;	//Solved

		var index = Seq[SeqNum];

		var possibles = Block[InBlock[index]] & Row[InRow[index]] & Col[InCol[index]];

		while (possibles) {

			var valbit = possibles & (-possibles);
			possibles &= ~valbit;

			board[index].value = bitcount(valbit);

			removeValbit(index, valbit);

			if (test(SeqNum+1)) return true;

			Block[InBlock[index]] |= valbit;
			Row[InRow[index]] |= valbit;
			Col[InCol[index]] |= valbit;
			}
		return false;		 	
	  }		


	function solve () {      
		setup();
		for (var i=0; i<81; i++) {
			if (board[i].value!=EMPTY) {
				var valbit2=1<<(board[i].value);
				removeValbit(i,valbit2);
			} else {
				Seq[Seq.length]=i;
			}
		}

		if (!test(0))
			alert("Cannot find solution");     
	}             

draw();

</script>


<p><button type="button" onclick="solve();">Solve!</button></p>
<p><button type="button" onclick="window.location.reload(true)">Clear</button></p>
