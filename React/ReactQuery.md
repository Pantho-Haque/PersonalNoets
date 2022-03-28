### install

```sh
    npm install react-query
```

### App.js

```sh
    import { QueryClient, QueryClientProvider } from 'react-query';
    import { ReactQueryDevtools } from 'react-query/devtools'
    import {ServerProvider} from "./server/server.context"

    const queryClient = new QueryClient()

    const App=()=>{
        return (
            <QueryClientProvider client={queryClient}>
                <ServerProvider>
                    <MainRoute />
                </ServerProvider>
                <ReactQueryDevtools initialIsOpen={false} />
            </QueryClientProvider>
        )
    }

```

```sh
import { useQuery } from 'react-query';

const {
    isLoading,
    data,
    isError,    // error occured or not
    error,      // error.message contains about the error
    isFetching, //
    refetch,    // a function to triger the fetching process

}=useQuery(

    "queryKey",

    ()=>{
        //fetching function who returns promise
    },

    {
        cacheTime: 5000, // after cachetime data will remove from cache
        staleTime: 0,   //  when component loads, after staletime data will fetched
        refetchOnMount:true, // refetching on every mounting. "always" can be a value
        refetchOnWindowFocus:true, // refetching when window achieves focus again
        refetchInterval: 2000 , // refetching after every 2sec.
        refetchIntervalInBackground:true, // continue to poll data when browser is not in focus

        enabled:false ,     // not automatically fetched data

        onSuccess:functionOnSuccess,    // fires the function after successfull fetching
        onError:functionPnError,        // fires the function after error occured

        select:(data)=>{                                           // transform into our desired data
            const superHeros= data.data.map(hero=>hero.name)
            return superHeros;
        }
    }

)
```

### Custom Query Hook

-> Hooks/useSuperHerosData.js

```sh
import { useQuery } from 'react-query';

const useSuperHerosData=(onSuccess,onError)=>{
    return useQuery("superheros",()={},{
        onSuccess,
        onError,
    })
}
```
