# HTTP Service

Angular 2 comes with an HTTP service we can use to retrieve from internet API. It returns an Observable.

This is the interface of the HTTP class from the angular 2 source.
```typescript
/**
     * Performs any type of http request. First argument is required, and can either be a url or
     * a {@link Request} instance. If the first argument is a url, an optional {@link RequestOptions}
     * object can be provided as the 2nd argument. The options object will be merged with the values
     * of {@link BaseRequestOptions} before performing the request.
     */
    request(url: string | Request, options?: RequestOptionsArgs): Observable<Response>;
    /**
     * Performs a request with `get` http method.
     */
    get(url: string, options?: RequestOptionsArgs): Observable<Response>;
    /**
     * Performs a request with `post` http method.
     */
    post(url: string, body: any, options?: RequestOptionsArgs): Observable<Response>;
    /**
     * Performs a request with `put` http method.
     */
    put(url: string, body: any, options?: RequestOptionsArgs): Observable<Response>;
    /**
     * Performs a request with `delete` http method.
     */
    delete(url: string, options?: RequestOptionsArgs): Observable<Response>;
    /**
     * Performs a request with `patch` http method.
     */
    patch(url: string, body: any, options?: RequestOptionsArgs): Observable<Response>;
    /**
     * Performs a request with `head` http method.
     */
    head(url: string, options?: RequestOptionsArgs): Observable<Response>;
```

## Using Http inside our app

To use http inside our application, we first need to include it in the module:
```typescript
...
import { HttpModule } from '@angular/http';

@NgModule({
  imports: [
    ...
    HttpModule
  ],
  declarations: [
    MyApp
  ],
  providers: [
  ],
  bootstrap: [MyApp]
})
export class MyAppModule {

}
```

Now, to use it inside a service, we can import `Http` from `@angular/http` and specify it to be injected into our service.

```typescript
import { Injectable } from '@angular/core';
import { Http } from '@angular/http';

@Injectable()
export class SpotifyService {
  spotifyUrl: String = 'https://api.spotify.com/v1/search?type=artist&q=';
  constructor (private http: Http) {}

  public getArtistsByQuery (query) {
    return this.http.get(`${this.spotifyUrl}${query}`).map(res => res.json())
  }
}
```

In this example, we will use the Spotify API to search artists by name. Also we will demonstrate how to use Observables to write a preview of results while typing.