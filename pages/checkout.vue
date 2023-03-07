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

<style scoped>
body {
  background-color: #fff;
  size: 100%;
  width: auto;
  height: auto;
  font-family: "Helvetica Neue",Helvetica,sans-serif;
  color: RGBA(0,0,0,0.8);
}

main {
  margin: 4px 0 0px 0;
  background-color: #f6f6f6;
  min-height: 90%;
  padding-bottom: 100px;
}

.hidden {
  display: none
}

.h-40 {
  height: 40px;
}

/* Shopping Cart Section - Start */
.shopping-cart {
  padding-bottom: 10px;
  overflow:hidden;
  transition: max-height 5s ease-in-out;
}

.shopping-cart.hide {
  max-height: 0;
  pointer-events: none;
}

.shopping-cart .content {
  box-shadow: 0px 2px 10px rgba(0, 0, 0, 0.075);
  background-color: white;
}

.shopping-cart .block-heading {
  padding-top: 40px;
  margin-bottom: 30px;
  text-align: center;
}

.shopping-cart .block-heading p {
  text-align: center;
  max-width: 600px;
  margin: auto;
  color: RGBA(0,0,0,0.45);
}

.shopping-cart .block-heading h1,
.shopping-cart .block-heading h2,
.shopping-cart .block-heading h3 {
  margin-bottom: 1.2rem;
  color: #BCA784;
}

.shopping-cart .items {
  margin: auto;
}

.shopping-cart .items .product {
  margin-bottom: 0px;
  padding-top: 20px;
  padding-bottom: 20px;
}

.shopping-cart .items .product .info {
  padding-top: 0px;
  text-align: left;
}

.shopping-cart .items .product .info .product-details .product-detail {
  padding-top: 40px;
  padding-left: 40px;
}

.shopping-cart .items .product .info .product-details h5 {
  color: #BCA784;
  font-size: 19px;
}

.shopping-cart .items .product .info .product-details .product-info {
  font-size: 15px;
  margin-top: 15px;
}

.shopping-cart .items .product .info .product-details label {
  width: 50px;
  color: #BCA784;
  font-size: 19px;
}

.shopping-cart .items .product .info .product-details input {
  width: 80px;
}

.shopping-cart .items .product .info .price {
  margin-top: 15px;
  font-weight: bold;
  font-size: 22px;
}

.shopping-cart .summary {
  border-top: 2px solid #C6E9FA;
  background-color: #F8F6F3;
  height: 100%;
  padding: 30px;
}

.shopping-cart .summary h3 {
  text-align: center;
  font-size: 1.3em;
  font-weight: 400;
  padding-top: 20px;
  padding-bottom: 20px;
}

.shopping-cart .summary .summary-item:not(:last-of-type) {
  padding-bottom: 10px;
  padding-top: 10px;
  border-bottom: 1px solid rgba(0, 0, 0, 0.1);
}

.shopping-cart .summary .text {
  font-size: 1em;
  font-weight: 400;
}

.shopping-cart .summary .price {
  font-size: 1em;
  float: right;
}

.shopping-cart .summary button {
  margin-top: 20px;
  background-color: #BCA784;
}

@media (min-width: 768px) {

  .shopping-cart .items .product .info .product-details .product-detail {
    padding-top: 40px;
    padding-left: 40px;
  }

  .shopping-cart .items .product .info .price {
    font-weight: 500;
    font-size: 22px;
    top: 17px;
  }

  .shopping-cart .items .product .info .quantity {
    text-align: center;
  }

  .shopping-cart .items .product .info .quantity .quantity-input {
    padding: 4px 10px;
    text-align: center;
  }
}

/* Card Payment Section - Start */
.container__payment {
  /*display: none;*/
}

.payment-form {
  padding-bottom: 10px;
  margin-right: 15px;
  margin-left: 15px;
  font-family: "Helvetica Neue",Helvetica,sans-serif;
}

.payment-form.dark {
  background-color: #f6f6f6;
}

.payment-form .content {
  box-shadow: 0px 2px 10px rgba(0, 0, 0, 0.075);
  background-color: white;
}

.payment-form .block-heading {
  padding-top: 40px;
  margin-bottom: 30px;
  text-align: center;
}

.payment-form .block-heading p {
  text-align: center;
  max-width: 420px;
  margin: auto;
  color: RGBA(0,0,0,0.45);
}

.payment-form .block-heading h1,
.payment-form .block-heading h2,
.payment-form .block-heading h3 {
  margin-bottom: 1.2rem;
  color: #BCA784;
}

.payment-form .form-payment {
  border-top: 2px solid #C6E9FA;
  box-shadow: 0px 2px 10px rgba(0, 0, 0, 0.075);
  background-color: #ffffff;
  padding: 0;
  max-width: 600px;
  margin: auto;
}

.payment-form .title {
  font-size: 1em;
  border-bottom: 1px solid rgba(0, 0, 0, 0.1);
  margin-bottom: 0.8em;
  font-weight: 400;
  padding-bottom: 8px;
}

.payment-form .products {
  background-color: #F8F6F3;
  padding: 25px;
}

.payment-form .products .item {
  margin-bottom: 1em;
}

.payment-form .products .item-name {
  font-weight: 500;
  font-size: 0.9em;
}

.payment-form .products .item-description {
  font-size: 0.8em;
  opacity: 0.6;
}

.payment-form .products .item p {
  margin-bottom: 0.2em;
}

.payment-form .products .price {
  float: right;
  font-weight: 500;
  font-size: 0.9em;
}

.payment-form .products .total {
  border-top: 1px solid rgba(0, 0, 0, 0.1);
  margin-top: 10px;
  padding-top: 19px;
  font-weight: 500;
  line-height: 1;
}

.payment-form .payment-details {
  padding: 25px 25px 15px;
  height: 100%;
}

.payment-form .payment-details label {
  font-size: 12px;
  font-weight: 600;
  margin-bottom: 15px;
  color: #8C8C8C;
  text-transform: uppercase;
}

.payment-form .payment-details button {
  margin-top: 0.6em;
  padding: 12px 0;
  font-weight: 500;
  background-color: #BCA784;
  margin-bottom: 10px;
}

.payment-form .date-separator {
  margin-left: 10px;
  margin-right: 10px;
  margin-top: 5px;
}

.payment-form a, .payment-form a:not([href]) {
  margin: 0;
  padding: 0;
  font-size: 13px;
  color: #BCA784;
  cursor:pointer;
}

.payment-form a:not([href]):hover{
  color: #3483FA;
  cursor:pointer;
}

#loading-message {
  display: none;
  text-align: center;
  font-weight: 700;
}

footer {
  padding: 2% 10% 6% 10%;
  margin: 0 auto;
  position: relative;
}

#horizontal_logo {
  width: 150px;
  margin: 0;
}

footer p a {
  color: #BCA784;
  text-decoration: none;
}

footer p a:hover {
  color: #3483FA;
  text-decoration: none;
}

@media (min-width: 576px) {
  .payment-form .title {
    font-size: 1.2em;
  }

  .payment-form .products {
    padding: 40px;
  }

  .payment-form .products .item-name {
    font-size: 1em;
  }

  .payment-form .products .price {
    font-size: 1em;
  }

  .payment-form .payment-details {
    padding: 40px 40px 30px;
  }

  .payment-form .payment-details button {
    margin-top: 1em;
    margin-bottom: 15px;
  }

  .footer_logo {
    margin: 0 0 0 0;
    width: 20%;
    text-align: left;
    position: absolute;
  }

  .footer_text {
    margin: 0 0 0 65%;
    width: 200px;
    text-align: left;
    position: absolute
  }

  footer p {
    padding: 1px;
    font-size: 13px;
    color: RGBA(0,0,0,0.45);
    margin-bottom: 0;
  }
}

@media (max-width: 576px) {
  footer {
    padding: 5% 1% 15% 1%;
    height: 55px;
  }

  footer p {
    padding: 1px;
    font-size: 11px;
    margin-bottom: 0;
  }
  .footer_text {
    margin: 0 0 0 45%;
    width: 180px;
    position: absolute
  }

  .footer_logo {
    margin: 0 0 0 0;
    position: absolute;
  }

}

/* Payment Result Section - Start */
.container__result {
  display: none;
}

#fail-response, #success-response {
  display: none;
}

.validation-error {
  border-color: red;
}

#validation-error-messages p {
  color: red;
}

</style>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'IndexPage'
})
</script>
