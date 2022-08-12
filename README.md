# Venipak-Shipping-Extension-for-OpenCart-2.x---3.x


## Short Description

This shipping extension allows you to define shipping to self-service post terminals "Venipak". Customers can select "Venipak" station's address from the list for Latvia, Estonia and Lithuania.


## Demonstration

Demo available:



* Frontend [https://opencartcart.com/venipakoc3/](https://opencartcart.com/venipakoc3/) (checkout to see available shipping methods).
* Backend <span style="text-decoration:underline;">https://opencartcart.com/venipakoc3/admin/index.php?route=extension/shipping/venipak</span>
    * username: `demo`
    * password: `demo`(without update permissions).


## Pre-Installation for Opencart version 3.0.3.6

Replace the system/modification.xml file with the modification file you can get here: [https://github.com/kenfai/opencart/blob/d31b4ebe3fd29dcc8861725d4934c6e3dd68e019/upload/system/modification.xml](https://github.com/kenfai/opencart/blob/d31b4ebe3fd29dcc8861725d4934c6e3dd68e019/upload/system/modification.xml)


## Installation And Setup For Opencart 3.x



1. Make backup of store files and database before you install the module (just a healthy habit).
2. Go to admin `Extensions -> Extension Installer` and upload file _venipak-shipping-3x_v.x.x.x.ocmod.zip_.
3. **_If You have Journal 3: _**

    1. add before


     			save: function (confirm) {
    			


    in catalog/view/theme/journal3/js/checkout.js


    this code:


    add before if you have Journal 3.0.x version:


    			saveVenipak: function (confirm) {
				this.error = {};

				//$('#venipak').prop('checked', '');
				if ($('#shipping_method_address_venipak').val()) {
					$('#venipak').attr('value', $('#shipping_method_address_venipak').val());
					this.$data.order_data['shipping_code'] = $('#shipping_method_address_venipak').val();
				} else {
					this.$data.order_data['shipping_code'] = 'venipak.venipak_0';
				}
				$('#venipak').prop('checked', 'checked');

				this.ajax({
					url: 'index.php?route=journal3/checkout/save' + (confirm ? '&confirm=true' : ''),
					data: {
						account: this.account,
						order_data: this.order_data,
						password: this.password,
						password2: this.password2,
						same_address: this.same_address,
						newsletter: this.newsletter,
						privacy: this.privacy,
						agree: this.agree,
						payment_address_type: this.payment_address_type,
						shipping_address_type: this.shipping_address_type,
						coupon: this.coupon,
						voucher: this.voucher,
						reward: this.reward
					},
					success: function (json) {
						this.update(json, confirm);
					}.bind(this)
				});
			},

    add before if you have Journal 3.1.x version:

       saveVenipak: function (confirm) {
                this.error = {};
                
                if (window['_QuickCheckoutAjaxSave']) {
                window['_QuickCheckoutAjaxSave'].abort();
                }
                
                if (confirm) {
                loader('.quick-checkout-wrapper', true);
                }
                
				//$('#venipak').prop('checked', '');
				if ($('#shipping_method_address_venipak').val()) {
					$('#venipak').attr('value', $('#shipping_method_address_venipak').val());
					this.$data.order_data['shipping_code'] = $('#shipping_method_address_venipak').val();
				} else {
					this.$data.order_data['shipping_code'] = 'venipak.venipak_0';
				}
				$('#venipak').prop('checked', 'checked');
                
                window['_QuickCheckoutAjaxSave'] = this.ajax({
                url: 'index.php?route=journal3/checkout/save' + (confirm ? '&confirm=true' : ''),
                data: {
                checkout_id: this.checkout_id,
                account: this.account,
                order_data: this.order_data,
                password: this.password,
                password2: this.password2,
                same_address: this.same_address,
                newsletter: this.newsletter,
                privacy: this.privacy,
                agree: this.agree,
                payment_address_type: this.payment_address_type,
                shipping_address_type: this.shipping_address_type,
                coupon: this.coupon,
                voucher: this.voucher,
                reward: this.reward
                },
                success: function (json) {
                window['_QuickCheckoutAjaxSave'] = null;
                this.update(json, confirm);
                }.bind(this)
                });
            },



    2. add after 


              this.shipping_methods = json.response.shipping_methods;


    this code:


    					this.venipak_addresses = json.response.venipak_addresses;


    3. https://go.venipak.lt/ws/get_pickup_points

4. Go to admin <code><em>Extensions -> Extensions -> [Shipping] -> Venipak</em></code> and click "<em>Install</em>" .
5. Find "Venipak" and click "Edit" .
6. <strong>A page will open with a form you need to fill:</strong>

![alt_text](https://partneris.lv/image/documentation/venipak-2x-3x/venipak-nr1.png)


7. 
    * General:
        * **Max. Dimensions (L x W x H)** - write maximum allowed product dimensions (➊);
        * **Max. Weight** - write max allowed product weight(➋);
        * **URL to CSV file for import addresses** - there will be an URL to CSV file for import "Venipak" addresses in Latvia, Lithuania and Estonia; This url may change in future, so you can then change it here(➌).
        * **Status** - select status "Enabled"(➍);
            * **Sort Order** - enter sort order(➎).
    * After that you need to fill fields in the each of geo zones (_Shipping Latvia_, _Shipping Lithuania_ and _Shipping Estonia_):

![alt_text](https://partneris.lv/image/documentation/venipak-2x-3x/venipak-nr2.png)


        * **Geo Zone**: Select the Geo Zone That represents the corresponding country (➊).
        * **Tax Class**: select tax class that will apply to cost(➋);
        * **Cost**: write cost for delivery(➌);
        * **Free shipping after: **write price after which is free shipping(➍);
        * **Status** - select status "Enabled" (➎).
8. Save changes by clicking "Save" (➏).

**Now you can use the module!**


### Checkout Screenshot


### Update "Venipak" destination addresses

![alt_text](https://partneris.lv/image/documentation/venipak-2x-3x/venipak-nr3.png")


1. Go to admin <code><em>Extensions->Extensions->[Shipping]->Venipak</em></code> and click "Edit" .
2. Click the button "Update addresses & Save". The list of available Venipak terminals will be updated from the link in URL to CSV file for import addresses (see Installation step 5).


## Extension upgrade



1. Install the new package following exactly the same steps described in the _Installation And Setup_ section above.

Release history



* 3.5.2: Apr 16, 2021: Initial version for Opencart 3.x
