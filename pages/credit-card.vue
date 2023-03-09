<template>
  <main>
    <input type="hidde" id="mercado-pago-public-key" value="${publicKey}" />

    <!-- Payment -->
    <section class="payment-form dark">
      <div class="container__payment">
        <div class="block-heading">
          <h2>Pagamento via cartão</h2>
          <p>Preencha o formulário abaixo para efetuar o pagamento de seu pedido através de um cartão de crédito</p>
        </div>
        <div class="form-payment">
          <div class="products">
            <h2 class="title">Resumo da compra</h2>
            <div class="item">
              <span class="price" id="summary-price"></span>
              <p class="item-name">
                <span>Mapa Astral </span> <span id="summary-quantity">1</span>x
              </p>
            </div>
            <div class="total">
              Total <span class="price" id="summary-total">R$ 49.90</span>
            </div>
          </div>
          <div class="payment-details">
            <form id="form-checkout">
              <h3 class="title">Informações do portador do certão</h3>
              <div class="row">
                <div class="form-group col">
                  <label for="form-checkout__cardholderEmail">E-mail</label>
                  <input id="form-checkout__cardholderEmail" name="cardholderEmail" type="email" class="form-control"/>
                </div>
              </div>
              <div class="row">
                <div class="form-group col-sm-5">
                  <label for="form-checkout__identificationType">Tipo de documento</label>
                  <select id="form-checkout__identificationType" name="identificationType" class="form-control"></select>
                </div>
                <div class="form-group col-sm-7">
                  <label for="form-checkout__identificationNumber">Numero do documento</label>
                  <input id="form-checkout__identificationNumber" name="docNumber" type="text" class="form-control"/>
                </div>
              </div>
              <br>
              <h3 class="title">Informações do cartão</h3>
              <div class="row">
                <div class="form-group col-sm-8">
                  <label for="form-checkout__cardholderName">Nome Impresso no Cartão</label>
                  <input id="form-checkout__cardholderName" name="cardholderName" type="text" class="form-control"/>
                </div>
                <div class="form-group col-sm-4">
                  <div class="expiration-date">
                    <label for="form-checkout__expirationDate">Validade</label>
                    <div id="form-checkout__expirationDate" class="form-control h-40"></div>
                  </div>
                </div>
                <div class="form-group col-sm-8">
                  <label for="form-checkout__cardNumber">Número do cartão</label>
                  <div id="form-checkout__cardNumber" class="form-control h-40"></div>
                </div>
                <div class="form-group col-sm-4">
                  <label for="form-checkout__securityCode">CVV</label>
                  <div id="form-checkout__securityCode" class="form-control h-40"></div>
                </div>
                <div id="issuerInput" class="form-group col-sm-12 hidden">
                  <label for="form-checkout__issuer">Emissor</label>
                  <select id="form-checkout__issuer" name="issuer" class="form-control"></select>
                </div>
                <div class="form-group col-sm-12">
                  <label for="form-checkout__installments">Parcelas</label>
                  <select id="form-checkout__installments" name="installments" type="text" class="form-control"></select>
                </div>
                <div class="form-group col-sm-12">
                  <input type="hidden" id="orderId" th:value="${order.id}" />
                  <input type="hidden" id="amount" th:value="${order.total}" />
                  <input type="hidden" id="description" th:value="${order.description}" />

                  <div id="validation-error-messages">
                  </div>

                  <br>

                  <button id="form-checkout__submit" type="submit" class="btn btn-primary btn-block">Efetuar pagamento</button>
                  <br>

                  <p id="loading-message">Loading, please wait...</p>
                  <br>
                </div>
              </div>

            </form>
          </div>
        </div>
      </div>
    </section>

    <!-- Result -->
    <section class="shopping-cart dark">
      <div class="container container__result">
        <div class="block-heading">
          <h2>Status do pagamento</h2>
          <p>Verifique abaixo o status de seu pagamento</p>
        </div>
        <div class="content">
          <div class="row">
            <div class="col-md-12 col-lg-12">
              <div class="items product info product-details">
                <div class="row justify-content-md-center">
                  <div class="col-md-4 product-detail">
                    <div class="product-info">
                      <div id="fail-response">
                        <br/>
                        <img th:src="@{/img/fail.png}" width="350px">
                        <p class="text-center font-weight-bold">Something went wrong</p>
                        <p id="error-message" class="text-center"></p>
                        <br/>
                      </div>
                      <div id="success-response" class="p-3">
                        <p><b>ID: </b><span id="payment-id"></span></p>
                        <p><b>Status: </b><span id="payment-status"></span></p>
                        <p><b>Detail: </b><span id="payment-detail"></span></p>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </main>
</template>


<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'IndexPage'
})
</script>
