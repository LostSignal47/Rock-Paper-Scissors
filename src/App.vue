<script setup>
import { ref,} from 'vue'

const win_count_player1 = ref(0)
const draw_count_player1 = ref(0)
const loss_count_player1 = ref(0)

const win_count_player2 = ref(0)
const draw_count_player2 = ref(0)
const loss_count_player2 = ref(0)



const control_game = {
	'ค้อน': {
		'ค้อน': 'เสมอ',
		'กระดาษ': 'แพ้',
		'กรรไกร': 'ชนะ',
    'ความรัก': 'แพ้'
	},
	'กระดาษ': {
		'ค้อน': 'ชนะ',
		'กระดาษ': 'เสมอ',
		'กรรไกร': 'แพ้',
    'ความรัก': 'แพ้'
	},
	'กรรไกร': {
		'ค้อน': 'แพ้',
		'กระดาษ': 'ชนะ',
		'กรรไกร': 'เสมอ',
    'ความรัก': 'แพ้'
	},
  'ความรัก': {
		'ค้อน': 'ชนะ',
		'กระดาษ': 'ชนะ',
		'กรรไกร': 'ชนะ',
    'ความรัก': 'เสมอ'
	}

}



const player1_choose = ref('');
const player2_choose = ref('');
const result = ref('');

// แก้ลิ้งค์รูปใหม่ด้วย
const choiceImages = {
  'ค้อน': 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSvX4oPEhb6xo6brx6BjLUVIAVnpNA8KyBUPqrs95o9i4mMdV9SxS47XysWSJvU9W4FnU0&usqp=CAU',
  'กระดาษ': 'https://media.tenor.com/MyDTT-w3aPAAAAAC/the-evidence.gif',
  'กรรไกร': 'https://pm1.aminoapps.com/6663/6ec005f7f3fe5502879b175f9b3f3cb04b375814_hq.jpg',
  'ความรัก': 'https://images-wixmp-ed30a86b8c4ca887773594c2.wixmp.com/f/09ec0fcd-ff32-4022-ae6c-d573c4a9b83c/dedf85z-bafb6b8e-4edf-46cf-9453-2432e515017e.gif?token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJ1cm46YXBwOjdlMGQxODg5ODIyNjQzNzNhNWYwZDQxNWVhMGQyNmUwIiwiaXNzIjoidXJuOmFwcDo3ZTBkMTg4OTgyMjY0MzczYTVmMGQ0MTVlYTBkMjZlMCIsIm9iaiI6W1t7InBhdGgiOiJcL2ZcLzA5ZWMwZmNkLWZmMzItNDAyMi1hZTZjLWQ1NzNjNGE5YjgzY1wvZGVkZjg1ei1iYWZiNmI4ZS00ZWRmLTQ2Y2YtOTQ1My0yNDMyZTUxNTAxN2UuZ2lmIn1dXSwiYXVkIjpbInVybjpzZXJ2aWNlOmZpbGUuZG93bmxvYWQiXX0.fz0gB6-tIMXephfi8oS0SfyOxl6JQMu8dl_K7CKLJC8',
};



function getRandomChoice() {
  const choices = ['ค้อน', 'กระดาษ', 'กรรไกร','ความรัก'];
  return choices[Math.floor(Math.random() * choices.length)];
}

function display_answer() {
  player1_choose.value = getRandomChoice();
  player2_choose.value = getRandomChoice();

  const out_result = control_game[player1_choose.value][player2_choose.value];

  if (out_result === 'ชนะ') {
    win_count_player1.value++;
    // loss_count_player2.value++;
    result.value = 'Player 1 ชนะ';
  } else if (out_result === 'แพ้') {
    win_count_player2.value++;
    // loss_count_player1.value++;
    result.value = 'Player 2 ชนะ';
  } else {
    // draw_count_player1.value++;
    // draw_count_player2.value++;
    result.value = 'เสมอ';
  }
}

function reset_round() {
  player1_choose.value = '';
  player2_choose.value = '';
  result.value = '';
  win_count_player1.value = 0;
  draw_count_player1.value = 0;
  loss_count_player1.value = 0;
  win_count_player2.value = 0;
  draw_count_player2.value = 0;
  loss_count_player2.value = 0;
}

</script>

<template>
  <div class="contrainer_all">
    <div class="box_title">
			<div class="text_title">เกมเป่ายิ๊งฉุบ แสนสนุก </div>
      </div>

      <div class="contrainer_game">
        <div class="box_1" id="box_play1">
          Player 1 : อัญเชิญ {{ player1_choose }}
          <img v-if="player1_choose" :src="choiceImages[player1_choose]" alt="Player 1 Choice" class="box_img"/>
        </div>
        <div class="box_2" id="box_play2">
          Player 2 : อัญเชิญ {{ player2_choose }}
          <img v-if="player2_choose" :src="choiceImages[player2_choose]" alt="Player 2 Choice" class="box_img" />
        </div>
      </div>

    <div class="start_buttom">
      <button @click="display_answer" class="buttom_start"> เป่ายิ๊งฉุบบบบบ </button>
    </div>

  <div class="contrainer_all_score"> 
    <div class="contrainer_score_1">
      <div class="box_score"> ผลการดวล <br> {{ result }}  </div>  
      <!-- <div class="box_score"> แต้มแพ้ Player1 <br> {{ loss_count_player1 }} </div>
        <div class="box_score"> แต้มเสมอ Player1 <br>{{ draw_count_player1 }} </div> -->
      </div>
      <div class="contrainer_score_2">
      <div class="box_score"> แต้มชนะ Player1 <br> {{ win_count_player1 }}  </div>  
      <div class="box_score"> แต้มชนะ Player2 <br> {{ win_count_player2 }}  </div>  
      <!-- <div class="box_score"> แต้มแพ้ Player2 <br> {{ loss_count_player2 }} </div>
      <div class="box_score"> แต้มเสมอ Player2 <br>{{ draw_count_player2 }} </div> -->
    </div>
  </div> 
    <div class="box_newgame">
      <button @click="reset_round" class="buttom_new"> เริ่มเกมใหม่ </button>
    </div>

  </div>    

</template>

