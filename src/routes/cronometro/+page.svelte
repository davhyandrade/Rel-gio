<script lang="ts">
    let horas = 0;
    let minutos = 0;
    let segundos = 0;

    let horasCronometro = '00';
    let minutosCronometro = '00';
    let segundosCronometro = '00';

    let isActiveCronometro = false;

    let interval: any;

    function formatDigit(digit: string) {
        if(parseInt(digit) < 10) {
            digit = '0'+digit;
            return digit;
        } else {
            return digit;
        }
    }

    function Cronometro() {
        segundos++;

        if(segundos === 60) {
            segundos = 0;
            minutos++;

            if(minutos === 60) {
                segundos = 0;
                minutos = 0;
                horas++;
            }
        }

        return [horasCronometro = formatDigit(horas.toString()), minutosCronometro = formatDigit(minutos.toString()), segundosCronometro = formatDigit(segundos.toString())];
    }

    function StartCronometro() {
        if(isActiveCronometro) return;
        isActiveCronometro = true;
        interval = setInterval(Cronometro, 1000)
    }

    function PauseCronometro() {
        isActiveCronometro = false;
        clearInterval(interval);
    }

    function ResetCronometro() {
        isActiveCronometro = false;
        clearInterval(interval);
        horas = 0;
        minutos = 0;
        segundos = 0;
        horasCronometro = '00';
        minutosCronometro = '00';
        segundosCronometro = '00';
    }
</script>

<svelte:head>
    <title>Cronômetro</title>
</svelte:head>

<div class="cronometro">
    <div class="horas-cronometro">
        <div>
            <h1>{horasCronometro}</h1>
            <span>Horas</span>
        </div>
        <span>:</span>
        <div>
            <h1>{minutosCronometro}</h1>
            <span>Minutos</span>
        </div>
        <span>:</span>
        <div>
            <h1>{segundosCronometro}</h1>
            <span>Segundos</span>
        </div>
    </div>
    <div class="field-buttons">
        <button on:click={StartCronometro}>Iniciar</button>
        <button on:click={PauseCronometro}>Pausar</button>
        <button on:click={ResetCronometro}>Parar</button>
    </div>
</div>

<style lang="scss">
  .cronometro {
    display: flex;
    flex-direction: column;
    align-items: center;
    color: gray;

    .horas-cronometro {
        display: flex;
        align-items: center;
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

    .field-buttons {
        width: 75%;
        position: absolute;
        bottom: 0;
        right: 0;
        display: flex;
        justify-content: space-between;
        border-top: 1px solid rgb(223, 223, 223);
        background: rgba(245, 245, 245, 0.053);
        
        @media screen and (max-width: 800px) {
            & {
                width: 100%;
            }
        }

        button {
            color: gray;
            width: 35%;
            padding: 20px 10%;
            border: none;
            cursor: pointer;
            font-size: 1rem;
            background: none;

            &:nth-child(1) {
                &:hover {
                    transition: 2s;
                    background: rgb(24, 71, 118, 0.6);
                    color: white;
                }

                &:active {
                    transition: 0.1s;
                    background: rgb(24, 71, 118, 0.8);
                    color: white;
                }
            }
            
            &:nth-child(2) {
                border-left: 1px solid rgb(223, 223, 223);
                border-right: 1px solid rgb(223, 223, 223);

                &:hover {
                    transition: 1s;
                    background: rgba(128, 128, 128, 0.316);
                    color: white;
                }

                &:active {
                    transition: 0.1s;
                    background: rgba(128, 128, 128, 0.7);
                    color: white;
                }
            }


            &:nth-child(3) {
                &:hover {
                    transition: 2s;
                    background: rgba(100, 3, 3, 0.6);
                    color: white;
                }

                &:active {
                    transition: 0.1s;
                    background: rgba(100, 3, 3, 0.8);
                    color: white;
                }
            }
        }
    }
  }
</style>