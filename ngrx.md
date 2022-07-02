# APM-Demo5

```
ACTION                      --------------->         REDUCER            --------------->               EFFECT     ......................... SELECT
                                                                                                                              
                                              const initialState: ProductState = {
                                                showProductCode: true,
                                                currentProductId: null,
                                                products: [],
                                                error: ''
                                              };

**  this.products$ = this.store.select(getProducts);
                                                                                                                            (1) state => state.products
**  this.store.dispatch(ProductPageActions.loadProducts());
(1) loadProducts
                                                                                        (2) ofType(ProductPageActions.loadProducts),
                                                                                            chargement des produits de la bdd
                                                                                            ACTION : loadProductsSuccess(products)
(3) loadProductsSuccess(products)
    paramètres : products                                                                                             
                                              (4) on(ProductApiActions.loadProductsSuccess)
                                                  update state avec : products
**  this.selectedProduct$ = this.store.select(getCurrentProduct);
                                                                                                                            (1) state => state.currentProductId
**  this.displayCode$ = this.store.select(getShowProductCode);
                                                                                                                            (1) state => state.showProductCode
**  checkChanged() { this.store.dispatch(ProductPageActions.toggleProductCode()); }
(1) toggleProductCode
                                              (2) on(ProductPageActions.toggleProductCode)
                                                  update state avec : showProductCode: !state.showProductCode

**  newProduct() { this.store.dispatch(ProductPageActions.initializeCurrentProduct()); }
(1) initializeCurrentProduct
                                              (2) on(ProductPageActions.initializeCurrentProduct
                                                  update state avec : currentProductId: 0

**  deleteProduct(product: Product) { this.store.dispatch(ProductPageActions.deleteProduct({ productId: product.id }) }
(1) deleteProduct
    paramètres :  productId
                                                                                        (2) ofType(ProductPageActions.deleteProduct)
                                                                                        Suppression du produit en bdd
                                                                                        ACTION : deleteProductSuccess({ productId })
(3) deleteProductSuccess
    paramètres :  productId
                                                (4) on(ProductApiActions.deleteProductSuccess
                                                    update state avec : 
                                                      products: state.products.filter(product => product.id !== action.productId),
                                                      currentProductId: null,
                                                      error: ''
                                                                                          

```    
