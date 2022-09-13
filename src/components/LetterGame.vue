<template>
    <button @click="reset">Start Over</button> <br/>
    <label for="life">timer:</label>
    <p name=life>{{ life }}</p>
    <label for="highestStreak">highest streak:</label>
    <p name=highestStreak>{{ highestStreak }}</p>
    <h2>{{ letter1 }}</h2>
    <div>
        <button @click="answer(true)" :disabled="gameOver">Before</button> or
        <button @click="answer(false)" :disabled="gameOver">After</button>
    </div>
    <h2>{{ letter2 }}</h2>
    <label for="score">score:</label>
    <p name="score">{{ score }}</p>
    <label for="streak">streak:</label>
    <p name=streak>{{ streak }}</p>
</template>

<script>
    export default {
        name: 'LetterGame',
        data() {
            return {
                letter1: '',
                letter2: '',
                isBefore: null,
                score: 0,
                streak: 0,
                highestStreak: 0,
                interval: null,
                life: 1000,
                gameOver: false,
            }
        },
        mounted() {
            this.generateLetters();
        },
        methods: {
            generateLetters() {
                if (this.interval) clearInterval(this.interval);
                this.currentTime = 0;

                const alphabet = "abcdefghijklmnopqrstuvwxyz".toUpperCase();
                let l1, l2;
                
                do {
                    l1 = alphabet[Math.floor(Math.random() * alphabet.length)];
                    l2 = alphabet[Math.floor(Math.random() * alphabet.length)];
                } while (l1 === l2);
                
                this.letter1 = l1;
                this.letter2 = l2;
                
                this.isBefore = l1.charCodeAt(0) - l2.charCodeAt(0) < 0;

                this.interval = setInterval(this.checkLife, 10);
            },
            checkLife() {
                if (--this.life !== 0) return;

                clearInterval(this.interval);
                this.gameOver = true;
            },
            answer(userAnswer) {
                if (this.isBefore === userAnswer) this.correctAnswer();
                else this.incorrectAnswer();
            },
            correctAnswer() {
                this.score++;
                this.streak++;
                this.life = 1000;

                if (this.streak > this.highestStreak) this.highestStreak = this.streak;

                this.generateLetters();
            },
            incorrectAnswer() {
                this.score--;
                this.streak = 0;

                this.generateLetters();
            },
            reset() {
                this.score = 0;
                this.life = 1000;
                this.gameOver = false;
                this.generateLetters();
            }
        }
    }
</script>