<template>
    <button @click="reset">Start Over</button> <br/>
    <label for="highestStreak">highest streak:</label>
    <p name=highestStreak>{{ highestStreak }}</p>
    <h2>{{ letter1 }}</h2>
    <div><button @click="answerBefore">Before</button> or <button @click="answerAfter">After</button></div>
    <h2>{{ letter2 }}</h2>
    <p>{{ `${letter1} ${isBefore ? 'comes' : 'does not come'} before ${letter2}` }}</p>
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
                answer: '',
                score: 0,
                streak: 0,
                highestStreak: 0,
            }
        },
        mounted() {
            this.generateLetters();
        },
        methods: {
            generateLetters() {
                const alphabet = "abcdefghijklmnopqrstuvwxyz".toUpperCase();
                let l1, l2;
                
                do {
                    l1 = alphabet[Math.floor(Math.random() * alphabet.length)];
                    l2 = alphabet[Math.floor(Math.random() * alphabet.length)];
                } while (l1 === l2);
                
                this.letter1 = l1;
                this.letter2 = l2;
                
                this.isBefore = l1.charCodeAt(0) - l2.charCodeAt(0) < 0;
            },
            answerBefore() {
                if (this.isBefore) this.correctAnswer();
                else this.incorrectAnswer();
            },
            answerAfter() {
                if (!this.isBefore) this.correctAnswer();
                else this.incorrectAnswer();
            },
            correctAnswer() {
                this.score++;
                this.streak++;

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
                this.generateLetters();
            }
        }
    }
</script>