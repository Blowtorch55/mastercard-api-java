# mastercard-api-java
MasterCard API SDK for Java.  See http://developer.mastercard.com

Overview:

MasterCard's Java SDK gives developers access to a host of powerful tools, including P2P Money transfers (MoneySend), 
locations of various merchants and ATMS (Locations), and the ability to detect potentially fraudulent 
transactions (Fraud Scoring). Calls to MasterCard's API are in accordance with OAuth 1.0 standards.


-------------------------------------------------------------------------------------------

Consumer Key/Private Key Acquisition:

Before beginning to use MasterCard's Java SDK, make sure you are a registered MasterCard developer and have a consumer and private key to use for your project:
	
	1. Go to developer.mastercard.com and click "Register" to register yourself for all of MasterCard's developer tools.

	2. Once registered, you will need both a Consumer Key and Private Key in order to use most of the MasterCard APIs. You can get a consumer key by going to the home screen, clicking on "Services", scrolling two-thirds of the way down the page, and clicking on "Go to My Dashboard". 

	3. Follow the instructions on this link - https://developer.mastercard.com/portal/display/api/Generating+RSA+Keys - to obtain both a Consumer Key and a .p12 file that contains your private key. 

	4. Make sure to store your .p12 file in the same directory as where you pulled the MasterCard SDK so that the private key is accessible from within your code.


-------------------------------------------------------------------------------------------

Code example


import com.mastercard.api.common.Environment;
import com.mastercard.api.restaurants.v1.domain.Restaurants;
import com.mastercard.api.restaurants.v1.domain.options.RestaurantsLocalFavoritesOptions;MerchantLocationRequestOptions;
import com.mastercard.api.restaurants.v1.services.RestaurantsLocalFavoritesService;

public class GetRestaurantsInArea {
	
	public static void main(String[] args)
	{
	    RestaurantsLocalFavoritesService service = new RestaurantsLocationServiceService(
            Environment.SANDBOX,
            getConsumerKey(), 
            getPrivateKey()
        );

        RestaurantsLocalFavoritesOptions options = new RestaurantsLocalFavoritesOptions(
             0,
             25
        )

        options.setCountry("USA");

        Restaurants restaurants = service2.getRestaurants(options2);
        List<Restaurants.Restaurant> list = restaurants.getRestaurantList();
        for (Restaurants.Restaurant r : list)
            System.out.println("Restaurant is " + r.getName());
	}
}

In addition to this code, you'll need helper classes/methods to get your consumer key and private key details

// return consumer key in String form

public String getConsumerKey()
{
    return "example-consumer-key";
}

// return the Private Key from the .p12 file

public PrivateKey getPrivateKey() {

        String fileName = "example-file.p12";
        String password = "password";
        KeyStore ks;
        Key key;
        try { ks = KeyStore.getInstance("PKCS12"); // get user password and file input stream
        ClassLoader cl = this.getClass().getClassLoader();
        InputStream stream = cl.getResourceAsStream(fileName);
        ks.load(stream, password.toCharArray());
        Enumeration<String> enumeration = ks.aliases();
        String keyAlias = enumeration.nextElement();
        key = ks.getKey(keyAlias, password.toCharArray());
        }
        catch (Exception e) {
            throw new MCApiRuntimeException(e);
        }
        return (PrivateKey) key;
    
    }


-------------------------------------------------------------------------------------------

API Reference

For a full API reference, head to the MasterCard Developer Zone: https://developer.mastercard.com/portal/display/api/API

Moreover, for code examples similar to the one above, you can also look at the test cases in this directory: https://github.com/MasterCard/mastercard-api-java/tree/master/src/test/java/com/mastercard/api

-------------------------------------------------------------------------------------------
