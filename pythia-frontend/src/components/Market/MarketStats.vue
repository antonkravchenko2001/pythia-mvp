<template>
    <div class="market-info">
        <div style="border-radius:5px;padding:15px;background:#102438">
            <div style="font-size: 20px;font-weight:500;margin-bottom:15px;">
                <span style="color:#a3b7ce;font-weight:400">Will </span> 
                <span>
                    {{marketData.marketInfo.asset.toUpperCase()}}
                </span>
                <span style="color:#a3b7ce;font-weight:400"> exceed </span> 
                <span>
                    {{marketData.marketInfo.strikePrice}} 
                </span>
                <span style="color:#a3b7ce;font-weight:400"> by </span> 
                <span>
                    {{_dateToStr(marketData.marketInfo.resolutionDate)}} 
                </span>
                <span style="color:#a3b7ce;font-weight:400"> ?</span> 
            </div>
            <div style="width:max-content; font-size: 13px">
                <span style="color:#a3b7ce">Wage Deadline: </span>
                <span style="color:white">{{_dateToStr(marketData.marketInfo.wageDeadline)}}</span>
            </div>
        </div>
        <div class="field-with-buttons">
            <div class="button-container">
                <button  ref='marketStats' name='marketStats'  @click="click('marketStats')" class="market-info-button" :class="{market: buttons.marketStats}" >Market Stats</button>
                <button v-if='$store.state.user' ref='myPortfolio' name='myPortfolio' @click="click('myPortfolio')" class="portfolio-info-button" :class="{portfolio: buttons.myPortfolio}">My Portfolio</button>
            </div>
            <div v-if='buttons.marketStats' class="item-val market-stats">
                <div>
                </div>
                <div class="market-info-text">No</div>
                <div class="market-info-text">Yes</div>
                <div class="market-info-text">Money Waged</div>
                <div class="market-stats-component no-annot">
                    {{round(marketData.marketInfo.moneyWaged[0])}}$
                </div>
                <div class="market-stats-component yes-annot">
                    {{round(marketData.marketInfo.moneyWaged[1])}}$
                </div>
                <div class="market-info-text">Shares Owned</div>
                <div class="market-stats-component no-annot">
                    {{round(marketData.marketInfo.sharesOwned[0])}}
                </div>
                <div class="market-stats-component yes-annot">
                    {{round(marketData.marketInfo.sharesOwned[1])}}
                </div>
            </div>
            <div v-if='buttons.myPortfolio' class="item-val market-stats">
                <div>
                </div>
                <div class="market-info-text">No</div>
                <div class="market-info-text">Yes</div>
                <div class="market-info-text">Money Waged</div>
                <div class="market-stats-component no-annot">
                    {{round(marketData.playerInfo.moneyWaged[0])}}$
                </div>
                <div class="market-stats-component yes-annot">
                    {{round(marketData.playerInfo.moneyWaged[1])}}$
                </div>
                <div class="market-info-text">Shares Owned</div>
                <div class="market-stats-component no-annot">
                    {{round(marketData.playerInfo.sharesOwned[0])}}
                </div>
                <div class="market-stats-component yes-annot">
                    {{round(marketData.playerInfo.sharesOwned[1])}}
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import { roundNum, dateToStr } from '../../utils.js';
    export default {
        props: ['marketData'],
        data(){
            return {
                buttons: {
                    marketStats: true,
                    myPortfolio: false
                }
            }

        },
        methods: {
            click(btn) {
                const buttonName = this.$refs[btn].name;
                if(!this.buttons[buttonName]){
                    this.buttons[buttonName] = true;
                    if(buttonName === 'myPortfolio'){
                        this.buttons.marketStats = false;
                    } else if(buttonName === 'marketStats') {
                        this.buttons.myPortfolio = false;
                    }
                }
            },
            round(num){
                return roundNum(num);
            },
            _dateToStr(dateStr){
                return dateToStr(dateStr);
            }
        },
    };
</script>


<style scoped>

    .market-info {
        display: flex;
        flex-direction:column;
        gap: 82px;
        justify-content: space-between;
        font-family: 'Montserrat';
        font-size: 15px;
        color: #ffffff;

    }
    .item-val {
        border: none;
        padding: 5px;
        color: #ffffff;
        font-weight: 300;
        border-radius: 5px;
        border-radius: 1px 1px 5px #121212;
        background: #102438;
    }

    .description-item-val {
        border: none;
        padding: 5px;
        color: #ffffff;
        font-weight: 300;
        border-radius: 5px;
        border-radius: 1px 1px 5px #121212;
        background: #102438;
        margin-left: 5px;
        margin-right: 5px;
        border: 1.2px solid #9287df;
    
    }

    .colored-border {
        border: 1.5px solid;
        border-color: #ffffff;
    }

    .field-with-buttons {
        display: grid;
        grid-template-columns: 1fr;
        grid-template-rows: 1fr 5fr;

    }

    .button-container {
        display: flex;
        justify-content: flex-end;
    }

    .market-info-button {
        font-size: 14px;
        background-color: transparent;
        margin-bottom: 5px;
        border: none;
        color: #ffffff;
    }

    .market {
        color: #9287df;
        margin-bottom: 0px;
    }

    .portfolio-info-button {
        font-size: 14px;
        background-color: transparent;
        margin-bottom: 5px;
        border: none;
        color: #ffffff;

    }

    .portfolio {
        color: #9287df;
        margin-bottom: 0px;
    }

    .market-stats {
       display: grid;
       background: #102438;
       row-gap: 10px;
       column-gap: 10px;
       grid-template-columns: 2fr 2fr 2fr;
       grid-template-rows: 0.3fr 1fr 1fr;
       padding: 15px;
    }

    .market-stats-component {
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 16px;
        font-weight: 500;
        height: 50px;
    }
    .market-info-text {
        display: flex;
        align-items: center;
    }

    .no-annot {
        border: #ec4d4dc2 1.2px solid;
        color: #ec4d4dc2;
        border-radius: 5px;
        background: #571f1f91;
    }

    .yes-annot {
        border: #4decc9c2 1.2px solid;
        color: #4decc9c2;
        border-radius: 5px;
        background: #1a5447c2;
    }
</style>