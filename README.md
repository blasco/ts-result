# ts-result
A simple typescript result monad implementation for the following abstraction

```ts
export interface Result<TSuccess1, TError1> {
  andThen<TResult extends Result<any, any>>(
    f: (value: TSuccess1) => TResult,
  ): Result<SuccessType<TResult>, TError1 | ErrorType<TResult>>;
  andThenAsync<TResult extends Result<any, any>>(
    f: (value: TSuccess1) => Promise<TResult>,
  ): Promise<Result<SuccessType<TResult>, TError1 | ErrorType<TResult>>>;
  catchError<TResult extends Result<any, any>>(
    f: (error: TError1) => TResult,
  ): Result<TSuccess1 | SuccessType<TResult>, ErrorType<TResult>>;
  catchErrorAsync<TResult extends Result<any, any>>(
    f: (error: TError1) => Promise<TResult>,
  ): Promise<Result<TSuccess1 | SuccessType<TResult>, ErrorType<TResult>>>;
  unwrapOrThrow(errorCallback?: (e: TError1) => void): TSuccess1;
}
```

Fur further details, check [this article](https://medium.com/@j2blasco).