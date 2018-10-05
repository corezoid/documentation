# Java

SDK for the work middleware.biz

https://github.com/corezoid/sdk-java/releases/tag/v2.1

```Java

import com.corezoid.sdk.entity.CorezoidMessage;
import com.corezoid.sdk.entity.RequestOperation;
import com.corezoid.sdk.utils.HttpManager;
import java.util.Arrays;
import java.util.List;
import net.sf.json.JSONObject;
import org.apache.http.HttpException;

public class MiddleWareModify {

    public static void main(String[] args) {
        try {
            // ID process
            String conv_id = "15476";
            // API user settings
            String apiLogin = "5965";
            String apiSecret = "VjKyfIuVAFOGGZwLLFfkHvrTPFUTBBP6E3A8596vIj5jiwqSsK";
            // ModifÏy task
            String ref = "test141874099180849";
            JSONObject data = new JSONObject()
                    .element("phone", "+380989055434")
                    .element("ref", "test141874099180849");
            RequestOperation operation = RequestOperation.modifyRef(conv_id, ref, data);
            // Add task to list
            List<RequestOperation> ops = Arrays.asList(operation);
            // Build a Message
            ConveyorMessage message = ConveyorMessage.request(apiSecret, apiLogin, ops);
            // Create HttpManager instance
            HttpManager http = new HttpManager();
            // Send all tasks to Middleware
            String answer = http.send(message);
        } catch (HttpException ex) {
            System.out.println(ex);
        }
    }

}

```
