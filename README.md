# Retrofit Rest API Calling

* APIInterface

      public interface ApiInterface {

        @POST("readContact.php")
        Call<List<Contact>> getContacts();
      }

* API Client

      public class ApiClient {

        public static final String BASE_URL = "http://192.168.8.100/android/";

        public static Retrofit retrofit;

        public static Retrofit getApiClient() {

            if (retrofit == null) {

                retrofit = new Retrofit.Builder().baseUrl(BASE_URL)
                        .addConverterFactory(GsonConverterFactory.create()).build();
            }
            return retrofit;
        }
      }
      
      
* Call In Your OnCreate()

      private ApiInterface apiInterface;
      

      apiInterface = ApiClient.getApiClient().create(ApiInterface.class);

        Call<List<Contact>> call = apiInterface.getContacts();

        call.enqueue(new Callback<List<Contact>>() {
            @Override
            public void onResponse(Call<List<Contact>> call, Response<List<Contact>> response) {
                contacts = response.body();
                adapter = new RecyclerAdapter(contacts);
                recyclerView.setAdapter(adapter);
            }

            @Override
            public void onFailure(Call<List<Contact>> call, Throwable t) {

            }
        });

# use below code to php


      <?php
      echo '[{"name":"Aruna","email":"aruna@abc.com"},{"name":"Kamal","email":"kaml@abc.com"}]';
      ?>
