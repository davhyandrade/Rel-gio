<script lang="ts">
    let horasRelogio = '00';
    let minutosRelogio = '00';
    let segundosRelogio = '00';
    
    function formatDigit(digit: string) {
        if(parseInt(digit) < 10) {
            digit = '0'+digit;
            return digit;
        } else {
            return digit;
        }
    }

    const relogio = setInterval(() => {
        let dateToday = new Date();
        horasRelogio = formatDigit(dateToday.getHours().toString());
        minutosRelogio = formatDigit(dateToday.getMinutes().toString());
        segundosRelogio = formatDigit(dateToday.getSeconds().toString());
    })
</script>

<svelte:head>
    <title>Relógio</title>
</svelte:head>

<div class="relogio">
    <div>
        <h1>{horasRelogio}</h1>
        <span>Horas</span>
    </div>
    <span>:</span>
    <div>
        <h1>{minutosRelogio}</h1>
        <span>Minutos</span>
    </div>
    <span>:</span>
    <div>
        <h1>{segundosRelogio}</h1>
        <span>Segundos</span>
    </div>
</div>

<style lang="scss">
    .relogio {
        display: flex;
        align-items: center;
        color: gray;
        margin-bottom: 50px;

        > span {
            font-size: 3rem;
            margin-bottom: 25px;
        }

        > div {
            display: flex;
            flex-direction: column;
            align-items: center;
            margin: 0 15px;

            h1 {
                font-size: 4rem;
                font-weight: normal;
            }

            @media screen and (max-width: 800px) {
                &:nth-child(1) {
                    margin-left: 0;
                }
            }
        }

        > div:nth-child(5) {
            margin-right: 0;
        }
    }
</style>