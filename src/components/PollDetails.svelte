<script>
    import Card from '../shared/Card.svelte';
    import PollStore from '../stores/PollStore.js';
    import Button from '../shared/Button.svelte';
    import { tweened } from 'svelte/motion';


    export let poll;

    // Reactive value
    $: totalVotes = poll.votesA + poll.votesB;
    $: percentA = Math.floor(100 / totalVotes * poll.votesA) || 0;
    $: percentB = Math.floor(100 / totalVotes * poll.votesB) || 0;

    // Tweened Percentages
    const tweenedA = tweened(0);
    const tweenedB = tweened(0);
    $:tweenedA.set(percentA);
    $:tweenedB.set(percentB);

    const upVote = (option, id) => {
        PollStore.update((data) => { 
            let copPolls = [...data]; // Capybara: Ok I pull up... ...the polls array and make a copy of it.

            const poll = copPolls.find(p => p.id === id);

            if (option === 'a') {
                poll.votesA++;
            } else {
                poll.votesB++;
            }

            return copPolls;
        });
    };

    const handledDelete = (id) => {
        PollStore.update(data => {
            return data.filter(p => p.id != id);
        });
    };
</script>

<Card>
    <div class="poll">
        <h3>{poll.question}</h3>
        <p>Total Votes: {totalVotes}</p>
        <div class="answer" on:click={() => upVote('a', poll.id)}>
            <div class="percent percent-a" style="width: {$tweenedA}%"></div>
            <span>{poll.answerA} ({poll.votesA})</span>
        </div>
        <div class="answer" on:click={() => upVote('b', poll.id)}>
            <div class="percent percent-b" style="width: {$tweenedB}%"></div>
            <span>{poll.answerB} ({poll.votesB})</span>
        </div>
        <div class="delete">
            <Button flat={true} type="red" on:click={() => handledDelete(poll.id)}>Delete</Button>
        </div>
    </div>
</Card>

<style lang="scss">
    .poll {
        user-select: none;
        h3 {
            margin: 0 auto;
            color: #555;
        }
        p {
            margin-top: 6px;
            font-size: 14px;
            color: #aaa;
            margin-bottom: 30px;
        }
        .answer {
            background-color: #fafafa;
            cursor: pointer;
            margin: 10% auto;
            position: relative;
            :hover {
                opacity: 0.6;
            }
            span {
                display: inline-block;
                padding: 10px 20px;
            }
            .percent {
                height: 100%;
                position: absolute;
                box-sizing: border-box;

            }
            .percent-a {
                border-left: 4px solid #d91b42;
                background-color: rgba(217, 27, 66, 0.2);
            }
            .percent-b {
                border-left: 4px solid #1b9e6a;
                background-color: rgba(0, 188, 212, 0.2);
            }
        }
        .delete {
            margin-top: 30px;
            text-align: center;
        }
    }
</style>