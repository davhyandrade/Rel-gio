<script lang="ts">
    import audioAlarme from '../../music/alarme.mp3';
    
    let horasTemporizador = '00';
    let minutosTemporizador = '00';
    let segundosTemporizador = '00';

    let horas = 0;
    let minutos = 0;
    let segundos = 0;

    let isActiveTemporizador = false;

    let interval: any;

    let data = {
        horas: '',
        minutos: '',
        segundos: ''
    };

    let isPiscando = false;
    
    function formatDigit(digit: string) {
        if(parseInt(digit) < 10) {
            digit = '0'+digit;
            return digit;
        } else {
            return digit;
        }
    }

    function Temporizador() {
        if(segundos === 0) {
            segundos = 60;

            if(minutos === 0) {
                minutos = 60;

                if(horas === 0) {
                    isPiscando = true;
                    setTimeout(() => {
                        isPiscando = false;
                    }, 3000);
                    document.querySelector<any>('audio').play();
                    clearInterval(interval);
                    ResetTemporizador();
                } else {
                    horas -= 1;
                }
            } else {
                minutos -= 1;
            }
        } else {
            segundos--;
        }


        return [horasTemporizador = formatDigit(horas.toString()), minutosTemporizador = formatDigit(minutos.toString()), segundosTemporizador = formatDigit(segundos.toString())];
    }

    function StartTemporizador() {
        if(horasTemporizador === '00' && minutosTemporizador === '00' && segundosTemporizador === '00') return;
        if(isActiveTemporizador) return;
        isActiveTemporizador = true;
        interval = setInterval(Temporizador, 1000)
    }
    
    function PauseTemporizador() {
        isActiveTemporizador = false;
        clearInterval(interval);
    }
    
    function ResetTemporizador() {
        isActiveTemporizador = false;
        clearInterval(interval);
        horas = 0;
        minutos = 0;
        segundos = 0;
        horasTemporizador = '00';
        minutosTemporizador = '00';
        segundosTemporizador = '00';
    }
    
    function StartModal() {
        document.querySelector<any>('dialog').showModal();
    }

    function OnKeyUp(event: any) {
        if(event.key === 'Enter'){
            StartModal();
        }
    }

    function handleDialog(event: Event) {
        event.preventDefault();
        horasTemporizador = formatDigit(data.horas || '0');
        minutosTemporizador = formatDigit(data.minutos || '0');
        segundosTemporizador = formatDigit(data.segundos || '0');
        horas = parseInt(horasTemporizador);
        minutos = parseInt(minutosTemporizador);
        segundos = parseInt(segundosTemporizador);
        document.querySelector<any>('dialog').close();
        data = {
            horas: '',
            minutos: '',
            segundos: ''
        };
    }
</script>

<svelte:head>
    <title>Cronômetro</title>
</svelte:head>

<audio src={audioAlarme}></audio>

<div class="Temporizador">
    <div on:keydown={OnKeyUp} on:click={StartModal} tabIndex="0" class={`horas-Temporizador ${isPiscando && 'piscando'}`}>
        <div>
            <h1>{horasTemporizador}</h1>
            <span>Horas</span>
        </div>
        <span>:</span>
        <div>
            <h1>{minutosTemporizador}</h1>
            <span>Minutos</span>
        </div>
        <span>:</span>
        <div>
            <h1>{segundosTemporizador}</h1>
            <span>Segundos</span>
        </div>
    </div>
    <div class="field-buttons">
        <button on:click={StartModal}>Adicionar</button>
        <button on:click={StartTemporizador}>Iniciar</button>
        <button on:click={PauseTemporizador}>Pausar</button>
        <button on:click={ResetTemporizador}>Parar</button>
    </div>
    <dialog>
        <form on:submit={handleDialog}>
            <div class="input-Temporizador">
                <div>
                    <input bind:value={data.horas} min={0} placeholder="00" type="number" name="horas" id="horas">
                    <span>Horas</span>
                </div>
                <span>:</span>
                <div>
                    <input bind:value={data.minutos} max={60} min={0} placeholder="00" type="number" name="minutos" id="horas">
                    <span>Minutos</span>
                </div>
                <span>:</span>
                <div>
                    <input bind:value={data.segundos} max={60} min={0} placeholder="00" type="number" name="segundos" id="horas">
                    <span>Segundos</span>
                </div>
            </div>
            <input type="submit" value="Enviar">
        </form>
    </dialog>
</div>

<style lang="scss">
  .Temporizador {
    display: flex;
    flex-direction: column;
    align-items: center;
    color: gray;

        .horas-Temporizador {
            display: flex;
            align-items: center;
            margin-bottom: 50px;
            cursor: pointer;
            transition: 1s;

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
                    > &:nth-child(1) {
                        margin-left: 0;
                    }
                }
            }

            > div:nth-child(5) {
                margin-right: 0;
            }
        }

        .piscando {
            animation: piscar 3s linear;
            color: rgb(24, 71, 118, 0.6);

            @keyframes piscar {
                0%{
                    opacity: 0;
                }
                25%{
                    opacity: 0.7;
                }
                40%{
                    opacity: 0;
                }
                50%{
                    opacity: 0.7;
                }
                65%{
                    opacity: 0;
                }
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
                padding: 20px 5%;
                border: none;
                cursor: pointer;
                font-size: 1rem;
                background: none;

                &:nth-child(2) {
                    border-left: 1px solid rgb(223, 223, 223);

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

                &:nth-child(3), &:nth-child(1) {
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


                &:nth-child(4) {
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

        dialog {
            left: 50%;
            top: 35%;
            margin: -125px -15%; 
            width: 30%;
            height: 250px;
            background: white;
            border-radius: 15px;
            overflow: hidden;
            border: 1px solid rgb(223, 223, 223);
            position: relative;

            @media screen and (max-width: 800px) {
                & {
                    width: 90%;
                    margin: -125px -45%;
                }
            }

            form {
                width: 100%;
                height: 250px;
                display: flex;
                flex-direction: column;
                align-items: center;
                justify-content: center;

                .input-Temporizador {
                    display: flex;
                    align-items: center;
                    margin-bottom: 50px;
                    color: gray;
                    width: 80%;

                    > span {
                        font-size: 3rem;
                        margin-bottom: 25px;
                    }

                    > div {
                        display: flex;
                        flex-direction: column;
                        align-items: center;
                        width: 45%;

                        input {
                            width: 70%;
                            background: transparent;
                            font-size: 4rem;
                            text-align: center;
                            border: none;
                            color: gray;
                            
                            &::-webkit-outer-spin-button, &::-webkit-inner-spin-button {
                                -webkit-appearance: none;
                            }

                            @media screen and (max-width: 800px) {
                                & {
                                    font-size: 3.2rem;
                                }
                            }
                        }
                    }

                    > div:nth-child(5) {
                        margin-right: 0;
                    }
                }

                > input {
                    position: absolute;
                    bottom: 0;
                    width: 100%;
                    background: transparent;
                    border-top: 1px solid rgb(223, 223, 223);
                    border-bottom: none;
                    border-left: none;
                    border-right: none;
                    cursor: pointer;
                    padding: 20px;
                    color: gray;
                    font-size: 1rem;

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
            }


            &::backdrop {
                background: rgba(128, 128, 128, 0.7);
            }
        }
    }
</style>